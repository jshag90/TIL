**제5편 import 와 export**

import {Component} from '@angular/core';

컴포너트, 서비스 등을 가져와서 사용 할 때 import로 지정

import {HomePage} from '../pages/home/home';

내가 만들 페이지도 지정 가능함



export class HomePage {

다른 곳에서 MyApp을 import해서 사용 할 수 있는도록 export 표시



**제6편 @Component**

@Component : 버튼 등 전반적인 로직을 말하며, 페이지 안에 포함 됨 



@Component Decorator

- 컴포넌트 + 데코레이터 = 컴포넌트 데코레이터

- 앵귤러2에서는 Decorator는 실험적인 구문이지만 아이오닉2에서는 정식 구문으로 사용함 

- "experimentalDecorators":true 옵션이 없으면 사용하지 못하지만 Ionic2 CLI가 알아서 관리해줌 

- 앵귤러에서 사용하는 Decorator와는 약간 다름

- 앵귤러 컴포넌트에서 사용하는 decorations 등을 ionic 컴포넌트에서는 사용하지 않음 

- 어떤것을 장식하는데 사용함

- 1) 클래스 앞에 @Component를 해주면 그 클래스는 컴포넌트가 됨

  ex) @Component() class ABC { .. } 

  ​      @Pipe class DEF{...} <-이는 Pipe를 만드는 Decorator

  ​

  2) 클래스 멤벼 변수 Decoration

  Decorator --장식--> @Input variable1 (갑을 입력 받음)

  ​				   @Output variable2(값을 내보냄)

@Componet{

selector : .. 컴포넌트를 어디에 표시 할지 결정

template : .. 컴포넌트 내용을 담는 곳

} 

@Componet{} <- 안에 들어가는 것을 메타데이터라고함

즉, 컴포넌트는 앱을 구성하는 요소나 로직을 말함

컴포넌트는 @Component Decorator로 장식된 클래스