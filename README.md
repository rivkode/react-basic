createElement 안에 들어가는 요소는 html태그와 같은 이름이어야 한다
html body에 react가 요소를 만들어줄텐데 이때 react dom을 사용한다
render는 사용자에게 보여주는 역할이다
Button 함수가 반환하는 것은 결국 element를 반환하는 것이다.


const container = React.createElement("div", null, [Title, Button]);
컴포넌트의 첫번째 글자는 항상 대문자여야 한다. 만약 소문자일 경우 HTML button 태그라고 React, JSX가 생각한다.

React js의 큰 장점은 UI에서 바뀐부분만 업데이트를 해주는 것이다. 이는 매우 큰 장점이다.
valina js에서는 모든 UI를 업데이트를 해주었다.
React js에서는 컴포넌트 단위로만 바꿀 수 있다.

정리

- JSX로 원하는 변수를 넣고싶을때에는 {counter} 과 같은 형태로 사용 가능하다.
- UI를 업데이트할때에는 ReactDOM.render()를 호출하면 된다.

애플리케이션 흐름

1. 애플리케이션이 처음 실행될떄 render를 호출한다.
2. render가 호출될때 이 함수는 Container컴포넌트들을 rood div 에 담아준다.
3. Container 함수가 호출되면 React Element가 반환된다.
4. React element는 Total click과 추가해준 변수를 가지고 있다.
5. 이때 변수 counter는 값이 0이다.
6. 그리고 등록한 click me라는 button 은 onClick이라는 eventListener를 등록해주었다.
7. 그 버튼을 클릭할때마다 countUp 이라는 함수가 실행된다
8. countUp 함수는 counter를 1씩 증가시키고 render()를 호출한다.
  - 이때 render()가 호출이 될때에는 처음부터 모든 Element를 생성하는 것이 아닌 변경된 부분에 대해서만 업데이트가 된다는 것이 중요하다.
  - 버튼을 클릭할때 Container 컴포넌트를 전체 리랜더링하는 것은 맞지만 HTML코드에서는 숫자만 바뀐다.
  - 이게 가능한 이유는 React js가 바뀐 부분에 대해서만 새로 생성할 수 있도록 하기 때문이다. 이것이 중요하다.
9. 결과적으로 1을 증가시키고 rerender를 하기 때문에 항상 최신 정보로 화면이 업데이트 된다.
10. 이때 화면 전체를 업데이트하는게 아닌 변경되는 데이터만 업데이트가 된다.
11. 이것이 React의 가장 큰 장점이다. Interactive 한 UI를 만들 수 있기 때문이다.

React에서 리렌더링 하는 방법

var, let, const 차이

var는 사용하지 않는 것이 좋다. 문제점이 있다.
var는 재할당 재선언이 자유롭게 가능하므로 문제점이 발생 가능성 높음

let은 재할당은 가능하지만 재선언은 불가하다.
다만 다른 범위 내에서는 재할당이 가능하다.
예를 들어 while문 안에서는 동일한 변수명에 대해 재선언이 가능하다.

const는 재할당, 재선언 모두 불가하다.

useState를 사용한 이후 흐름

1. counter라는 데이터를 받아서 return 에 Total clicks에 해당 데이터를 {counter} 로 받고 있다.
2. 이 return 부분이 사용자가 보게 될 컴포넌트 이다.
3. click이 발생하면 onClick 함수를 통해 setCounter가 호출된다.
4. 이때 counter의 새로운 값을 가지고 setCounter 함수가 호출된다.
5. setCounter 함수가 호출이 될때에는 render도 함께 된다.
6. render가 되는 것을 React.useState가 해주고 있다.


modifier 함수를 가지고 state를 변경할 때 컴포넌트가 재생성된다.
새로운 값을 가지고 리렌더링 된다.

modifier 함수를 사용해 state 데이터를 바꿀 때 컴포넌트 전체가 재생성된다.
이때 새로운 값을 가지고 생성된다.

하지만 React js는 매 순간 컴포넌트에 대해 이벤트리스너를 다시 등록하거나 새로운 Total Click을 만드는게 아니라 변경된 부분에 대해서만 바뀐다.

Virtual Dom

가상 돔은 실제 돔의 모두를 변경하기에는 자연스럽지 못하고 비용이 크기때문에 변경된 부분에 대해서만 반영하기 위해 나타난 개념이다.

그래서 React는 변경사항이 발생할때 가상돔을 먼저 그리고 실제 돔과 비교하는 과정을 통해 변경된 부분에 대해서만 변경을 반영한다.

그래서 실제 UI에서는 전체를 변경하는 것이 아니라 변경된 부분만 변경될 수 있다.

값을 세팅하고 변경하는 함수를 설정하는 코드는

1. const [counter, setCounter] = React.useState(0);

1. setCounter(counter + 1)
2. setCounter((current) => current + 1)

여기서 counter는 변수 이름이고, setCounter는 변경할 수 있는 함수이다.
React.useState(0)를 하면 초기값인 0으로 변수가 세팅되고, 이 변수를 변경할 수 있는 함수 f 가 2번째 인자로 주어지며 이를 setCounter과 같이 세팅하면 이후에 setCounter(counter + 숫자)로 접근할 수 있다.

렌더링은 modifier가 해주는 건가 ?

modifier 함수가 렌더링을 해주는것은 아니지만 modifier를 통해 변경하면 트리거가 발생되어 React가 컴포넌트 함수를 다시 호출하고 가상돔을 새로 만든다. 새로만든 가상돔과 실제 돔을 비교하여 변경된 부분에 대해서만 렌더링되어 화면에 나타난다.

사용자 입력으로부터 들어온 값을 실제 React의 변수로 연결해주는 작업은 ?

<input> 에 value={minutes} 로 등록하면 된다.

사용자가 입력하였을떄 결국 이벤트기반으로 동작하기 때문에 onChange 를 지운다면 ?
사용자가 입력한 이벤트를 감지할 수 없으므로 default 값인 0으로 그대로 유지된다.