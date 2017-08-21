Template Statement는 element, component, directive의 이벤트에 반응



//element, component, directive

{{abc}}

" var1"

변수 = "값"

\<div [속성] = "Template Expression"> ---> property binding

\<div (이벤트) = "Template Statement" > ---> event binding

\<div (click) ="onClick()">

new ++ == += -= | & 는 쓸수 없음.

=

, ; 을 통한 chaning을 할 수 있음

\<div *ngIf = "active">

=을 중간에 두고, 왼쪽에 이벤트 오른쪽에 표현

(Template Statement) 

(event) = "handler()"



*ngIf -> 화면에 내용을 감추거나 보여주고자 할 때 사용

\<div *ngIf ="show">

Hello World!

\</div>



---------------------------------------------------------

export class HomePage{

​	show : boolean = false;

​	constructor(){}

}

--------------------------------------------------------------------------------------------

*ngFor 는 배열의 요소를 화면에 나타낼 때 사용

------

export class HomePage{

​	myPets=[

{

kind : 'cat',

name:'Nabi',

color : 'white'

},

{

kind : 'Dog',

name : 'Happy',

color : 'brown'

}

]

​	constructor(){}

}

-------------------------------------------------------------------------------------------

\<div *ngFor = " let pet of myPets; let i=index">

나의 {{ i+1}} 번째 애완동물 \<br>

\<b>종류\</b>:{{pet.kind}}\<br>

\<b>이름\</b>:{{pet.name}}\<br>

\<b>색깔\</b>:{{pet.color}}\<br>

\</div>

--------------------------------------------------------------------------------------------export class HomePage{

​	myPets={

nabi : {

kind : 'cat',

name:'Nabi',

color : 'white'

},

happy : {

kind : 'Dog',

color : 'brown'

}

};

​	constructor(){}

}

--------------------------------------------------------------------------------------------

위와 같은 객체 변수에서는 Iterable하지 않으므로 출력해주지 못하고 에러가 발생한다.

이를 해결하기 위해서는 객체들을 배열에 넣어준다. 

\<div *ngFor = " let pet of myPets; let i=index">

나의 {{ i+1}} 번째 애완동물 \<br>

\<b>종류\</b>:{{pet.kind}}\<br>

\<b>이름\</b>:{{pet.name}}\<br>

\<b>색깔\</b>:{{pet.color}}\<br>

\</div>

--------------------------------------------------------------------------------------------

export class HomePage{

​	myPets={

nabi : {

kind : 'cat',

name:'Nabi',

color : 'white'

},

happy : {

kind : 'Dog',

color : 'brown'

}

};

​	constructor(){}

get pets(){

return Object.keys(this.myPets);

}

}

--------------------------------------------------------------------------------------------\<div *ngFor = " let name of pets; let i=index">

나의 {{ i+1}} 번째 애완동물 \<br>

\<b>종류\</b>:\{{myPets\[name]['kind'] }}\<br>

\<b>색깔\</b>:\{{myPets\[name]['color'] }\<br>

\</div>

--------------------------------------------------------------------------------------------

**Property Binding**

\<div [DOM 속성]="클래스속성">



\<img [src]="urlFall">

--------------------------------------------------------------------------------------------

export class HomePage{

​	urlFall: string = "assests/fall.png";

​	urlImage: Array<string> = [

​	'assets/fall.png',

​	'assets/fall.jpg'

​	];

​	constructor(){

​		let index = 0;

​		setInterval() => {

​			index = idex == 0?1:0;

​			this.urlFall = this.urlImages[index];

​		}

​		, 1000);

​	}

}

---------------------------------------------------------------------------------------	constructor(){

​		setTimeout(() =>

​		this.urlFall="assets/fall.jpg"

​		,1000 );

​	}