**event binding**

주로 컴포넌트 클래스와 이벤트을 연결

\<button ion-button (click)="onClickHello()">HELLO\</button>

-------------------------------------------------------------------------------------

export class HomePage{

​	message : Array\<str>

​	constructor(public navCtrl : NavController)

​	onClickHello(){

​		alert("Hello World");

​	}

}

-----------------------------------------------------------------------------------

\<ion-list>

​	\<ion-item>

​		\<ion-input #message (keyup enter) = "message.push(message.value); messag.value=''">

​		\</ion-input>

\</ion-item>

\<ion-item *ngFor=" let msg of messages.reverse()">

​	{{msg}}

\</ion-item>

\</ion-list>

------

export class HomePage{

​	message : Array\<str>

​	constructor(public navCtrl : NavController)

​	onClickHello(){

​		alert("Hello World");

​	}

}

-----------------------------------------------------------------------------------

**One way Binding, Two Way Binding**

One way Binding의 예

\<img [src]="url">

\<button (click)="onClick()">

-----------------------------------------------------------------------------------

export class HomePage{

​	url : string = "abc.jpg";

​	constructor(public navCtrl)

}

*url 변수의 값을 src로 넣을 수 있지만, src의 값을 url 변수로 넣을 수 없음

*어떠한 event 값을 한쪽 값으로만 전달하는 것

----------------------------------------------------------------------------------

Two Way Binding의 예

\<input [(ngModel)]="abc">

{{abc}}

-----------------------------------------------------------------------------------

export class HomePage{

abc : string = "Hello World!";

constructor(public navCtrl : NavController){

​	setInterval(() => console.log(this.abc),1000);

}

}

*input box의 값을 가져올수도 있고 넘겨 줄수도 있음

*form 항목에서 사용 가능

----------------------------------------------------------------------

**Template Reference**

tempalte reference variable;

템플릿 레퍼런스 변수는 템플릿 항목을 사용 할 수 있게 해주는 변수

\<input #phone (keyup)="call = phone.value">

{{ call }}

*변수 명으로 해당 항목을 사용할 수 있게함

----------------------------------------------------------------------

**@ViewChild**

@ViewChild는 템플리시 만들어지기 전에 참조 가능



\<button ion-button (click)="onClickScroll()"> SCROLL \</button>



\<h1 *ngFor = " let i of [1,2,3,4,5,6,7,8,9,10]">

​	Count : {{i}}\<br/>

\</h1>

----------------------------------------------------------------------

import { Component, ViewChild} from '@angluar'}

import {Content} from 'ionic-angular';

@Component({

 templateUrl :'home.html'

})

export class  HomePage{

​	y:number = 0 ;

​	@ViewChild(Content) content: Content;	

​	onClickScroll(){

​	this.content.scrollTo(0, this.y+=80, 100);

​	}

}

*클래스 초기화 과정이 아닌 탬플릿이 생성된 후에는 @ViewChild가 필요 없음.

----------------------------------------------------------------------

**Directive**

DOM 항목 또는 HTML 태그에 새로운 기능을 부여 할 때 사용

{{abc | json}}

\<h1 *ngIf = "abc">

​	Hello World

\</h1>

----------------------------------------------------------------------

export class HomePage{

​	abc: boolean = true;

​	constructor(){

​	}

}

----------------------------------------------------------------------

\<h1 heiglight>

​	Hello World

\</h1>

*component 폴더에 directive를 만듬

------

import{Directive, ElementRef, Renderer} from '@angular/core'

@Directive({

​	'selector' : '[highlight]'

})

export class Hightlight{

​	constructor( el: ElementRef, renderer : Renderer){	

​	renderer.setElmentStyle(el.nativeElement, 'background','blue')

​	}

}

*app.module.ts에서 import를 시켜야함

----------------------------------------------------------------------

import{Directive, ElementRef, Renderer} from '@angular/core'

@Directive({

​	'selector' : '[highlight]'

})

export class Hightlight{

​	constructor( el: ElementRef){	

​		el.nativeElement.style.color="orange";

​		el.nativeElement.style.backgroundColor="grary";

​	}

}

----------------------------------------------------------------------

import {Highlight} from '../components/highlight'

@NgModule({

})

export class HomePage{

​	abc: boolean = true;

​	constructor(){

​	}

}

----------------------------------------------------------------------

**Child Componet**

* 자식 컴포넌트는 일반 컴포넌트와 매우 비슷(차이 있음)
* 자식 컴포넌트의 selector를 부모 컴포넌트에 사용하면 자식 컴포넌트 템플릿이 부모 컴포넌트 템플릿에 표시 됨
* ionic g component child-cat => ionic CLI가 알아서 만들어줌

----------------------------------------------------------------------

child-cat.ts

child-cat.html

-----------------------------------------------------------------------------------------------------------------------------------------------------------

**child-cat.ts** 생성

import{ Component } from '@angular/core';

@Component({

​	selector : 'child-cat',

​	templateUrl : 'child-cat.html'

})

export class childCat{

​	no: number = 0;

​	onClickNo(){

​		this.no ++;

​	}

}

----------------------------------------------------------------------

child-cat.html 생성

\<h2 (click) = "onClickNo()">

​	No. of Child cat : {{ no }}

\</h2>

----------------------------------------------------------------------

app.module.ts에 ChildCat을 import 추가 

----------------------------------------------------------------------

home.html에서 사용

\<child-cat>\</child-cat>















