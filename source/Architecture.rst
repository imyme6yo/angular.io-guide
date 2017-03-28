H1 -- ARCHITECTURE OVERVIEW

Angular 앱의 기본 요소

Angular는 HTML와 JavaScript 또는 JavaScript로 컴파일 되는 TypeScript와 같은 언어로 클라이언트 앱을 만드는 프레임워크이다.

프레임워크는 몇몇은 코어, 몇몇은 선택적으로 사용가능한 라이브러리들로 이뤄져 있다.

Angular 마크업이 있는 HTML템플릿과 템플릿을 관리하는 컴포넌트 클래스, 서비스의 추가적인 앱 로직, 컴포넌트와 서비스를 포함하고 있는 모
듈로 Angular 앱을 작성한다.

(Angular 앱은 템플릿, 컴포넌트, 서비스 그리고 모듈로 이뤄져 있다.)

root 모듈을 부트스트랩해 앱을 실행한다. Angular은 브라우저에 앱의 콘텐츠를 보여주고 사용자와 상호작용 한다.

물론 이 것 이외의 내용도 있다. 자세한 내용은 이 문서에서 다룰 것이다. 지금은 큰 그림에 주목하자.

구조에 대한 그림은 Angular 앱의 8개의 주요 구성요소를 보여준다

'Modules<https://angular.io/docs/ts/latest/guide/architecture.html#modules>'_
'Components<https://angular.io/docs/ts/latest/guide/architecture.html#components>'_
'Templates<https://angular.io/docs/ts/latest/guide/architecture.html#templates>'_
'Metadata<https://angular.io/docs/ts/latest/guide/architecture.html#metadata>'_
'Data binding<https://angular.io/docs/ts/latest/guide/architecture.html#data-binding>'_
'Directives<https://angular.io/docs/ts/latest/guide/architecture.html#directives>'_
'Services<https://angular.io/docs/ts/latest/guide/architecture.html#services>'_
'Dependency injection<https://angular.io/docs/ts/latest/guide/architecture.html#dependency-injection>'_

위의 구성요소에 대해서 알아볼 것이다.

이 문서의 코드들은 'live example'_과 '예제 코드 다운로드'_ 에서 확인할 수 있다.

.. _live example: https://angular.io/resources/live-examples/architecture/ts/eplnkr.html
.. _예제 코드 다운로드: https://angular.io/resources/zips/architecture/architecture.zip

H2 -- Modules

angular 앱은 모듈로 이뤄져 있으면 Angular는 Angular 모듈 또는 NgModule이라고 불리는 모듈화 시스템을 가지고 있다.
Angular Module은 다룰 내용이 많다. 여기서는 단지 모듈에 대해서 소개만 한다. 'Angular Modules'_ 페이제에서 좀 더 자세히 다룰 것이다.

.. _Angular Modules: https://angular.io/docs/ts/latest/guide/ngmodule.html

모든 Angular 앱은 최소 하나의 모듈 클래스 'root module'_을 가지며 편의상 이름을 AppModule이라고 이름 짓는다.

.. _root module: https://angular.io/docs/ts/latest/guide/appmodule.html

작은 앱은 root 하나로 이뤄진 반면 대부분의 앱은 많은 기능 모듈로 이뤄져 있다.

루트 또는 기능 하나의 Angular 모듈은 은 @NgModule 데코레이터를 가지는 클래스이다.

::
데코레이터는 JavaScript 클래스들을 변경하는 함수이다. Angular는 클래스에 메타데이터를 추가해 클래스가 어떠한 의미를 가지고 어떻게 동작하는지 알려주는 많은 데코레이터를 가지고 있다. 웹에 데코레이터에 대에서 '더 많은 내용'_들이 있다
.. _더 많은 내용: https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841#.x5c2ndtx0
::

gModule은 모듈에 대한 속성을 가지고 있는 하나 메타데이터 객체를 가지는 데코레이터 함수이다. 중요한 속성들은 다음과 같다:

    * declarations - 모듈에 포함되는 뷰 클래스들이다. Angular는 3가지의 뷰클래스들을 가지고 있다: '컴포넌트'_, '디렉티브'_, '파이프'_
.. _컴포넌트: https://angular.io/docs/ts/latest/guide/architecture.html#components
.. _디렉티브: https://angular.io/docs/ts/latest/guide/architecture.html#directives
.. _파이프: https://angular.io/docs/ts/latest/guide/pipes.html
    * exports - 다른 모듈의 컴포넌트 템플릿에서 접근해 사용가능한 declarations의 뷰클래스들의 부분집합이다.

    * imports - export한 클래스들 현재 모듈의 컴포넌트 템플릿에서 필요한 다른 모듈들

    * providers - 서비스의 전역 집합을 제공하는 서비스들의 생성자 이다;서비스들은 앱의 모든 부분에서 접근이 가능하게 된다.

    * bootstrap - 루트 컴포넌트라고 불리는 앱의 첫 화면이다. 다른 화면들을 가지고 있다. 오직 루트 모듈만 bootstrap 속성에 설정한다.

아래는 간단한 root 모듈 이다: