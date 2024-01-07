### 상태 관리는 왜 필요한가?
웹 애플리케이션에서 상태로 분류될 수 있는 것들은 대표적으로 다음과 같은 것이 있습니다.
- UI: 기본적으로 웹 애플리케이션에서 상태라 함은 상호 작용이 가능한 모든 요소의 현재 값을 의미합니다. 다크/라이트 모드, 라디오를 비롯한 각종 input, 아림창의 노출 여부 등 많은 종류의 상태가 존재한다.
- URL: 브라우저에서 관리되고 있는 상태값으로 여기에도 우리가 참고할 만한 상태가 존재할 수 있습니다. https://www.airbnb.co.kr/rooms/34113796?adults=2와 같은 주소가 있다고 가정해 봅시다. 이 주소는 roomId=34113796과 adults=2라고 하는 상태가 존재하며 이 상태는 사용자의 라우팅에 따라 변경됩니다.
- 폼(form): 폼에도 상태가 존재합니다. 로딩 중인지, 현재 제출됐는지, 접근이 불가능한지, 값이 유효한지 등 모두가 상태로 관리됩니다.
- 서버에서 가져온 값: 클라이언트에서 서버로 요청을 통해 가져온 값도 상태로 볼 수 있습니다. 대표적으로 API 요청이 있습니다.

애플리케이션 전체적으로 관리해야 할 상태가 있다고 가정해 봅시다. 그리고 그 상태에 따라 다양한 요소들이 각 상태에 맞는 UI를 보여줘야 합니다. 상태를 어디에 둘 것인가? 전역 변수에 둘 것인가? 별도의 클로저를 만들 것인가? 그렇다면 그 상태가 유효한 범위는 어떻게 제한할 수 있을까? 상태의 변화에 따라 변경돼야 하는 자식 요소들은 어떻게 이 상태의 변화를 감지할 것인가?

이러한 상태 변화가 일어남에 따라 즉각적으로 모든 요소들이 변경되어 애플리케이션이 찢어지는 현상(이를 tearing이라고 하며, 하나의 상태에 따라 서로 다른 결과물을 사용자에게 보여주는 현상을 말한다)을 어떻게 방지할 것인가?

### 리액트 상태 관리의 역사
**Flux 패턴의 등장**<br>
우리가 순수 리액트에서 할 수 있는 전역 상태 관리 수단이라고 한다면 Context API를 떠올릴 것입니다(엄밀히 이야기하면 리액트 Context API는 상태 관리가 아니라 상태 주입을 도와주는 역할입니다).<br>
그러나 리액트에서 Context API가 선보인 것은 16.3 버전이었습니다. 그 전까지는, 리덕스가 나타나기 전까지 리액트 애플리케이션에서 딱히 이름을 널리 알린 상태 관리 라이브러리는 없었습니다.<br>
그러던 중 2014년 경, 리액트의 등장과 비슷한 시기에 Flux 패턴과 함께 이를 기반으로 한 라이브러리은 Flux를 소개하게 됩니다.<br>
Flux에 대해 소개하기에 앞서 먼저 이 당새 웹 개발 상황을 짚고 넘어갑시다. 웹 애플리케이션이 비대해지고 상태(데이터)도 많아짐에 따라 어디서 어떤 일이 일어나서 이 상태가 변했는지 등을 추적하고 이해하기가 매우 어려운 상황이었습니다.<br>
페이스북 팀은 이러한 문제의 원인을 양방향 데이터 바인딩으로 봤습니다. 뷰(HTML)가 모델(자바스크립트)을 변경할 수도 있으며, 반대의 경우 모델도 뷰를 변경할 수 있습니다.<br>
이는 코드를 작성하는 입장에서는 간단할 수 있지만 코드의 양이 많아지고 변경 시나리오가 복잡해질수록 과리가 어려워집니다.<br>
페이스북 팀은 **양방향이 아닌 단방향으로 데이터 흐름을 변경하는 것을 제안하는데 이것이 바로 Flux패턴의 시작**입니다.<br>

먼저 각 용어의 정의를 살펴봅시다.<br>
- 액션: 어떠한 작업을 처리할 액션과 그 액션 발생 시 함께 포함할 데이터를 의미합니다. 액션 타입과 데이터를 각 각 정의해 이를 디스패처로 보냅니다.
- 디스패처: 액션을 스토어에 보내는 역할을 합니다. 콜백 함수 형태로 앞서 액션이 정의한 타입과 데이터를 모두 스토어에 보냅니다.
- 스토어: 여기에서 실제 상태에 따른 값과 상태를 변경할 수 있는 메서드를 가지고 있습니다. 액션의 타입에 따라 어떻게 이를 변경할지가 정의돼 있습니다.
- 뷰: 리액트의 컴포넌트에 해당하는 부분으로, 스토어에서 만들어진 데이터를 가져와 화면을 렌더링하는 역할을 합니다.

```js
type StoreState = {
  count: number
}

// type은 action의 종류
// payload는 어떤 데이터를 필요로 하는지
type Action = { type: 'add'; payload: number }

// 스토어
// 상태에 따른 값이 어떻게 변경되는지
function reducer(prevState: StoreState, action: Action) {
  const { type: ActionType } = action
  if (Action Type === 'add') {
    return {
      count: prevState.count + action.payload
    }
  }
  throw new Error(`Unexpected ACtion [${ActionType}]`)
}

// 뷰
export default function App() {
  // useReducer의 첫번째 인자: 스토어
  // useReducer의 두번째 인자: 현재 상태
  const [state, dispatcher] = useReducer(reducer, { count: 0 })

  function handleClick() {
    // 액션 실행
    dispatcher({ type: 'add', payload: 1 })
  }

  return (
    <div>
      <h1>{state.count}</h1>
      <button onClick={handleClick}>+</button>
    </div>
  }
}
```
이러한 단방향 데이터 흐름 방식은 당연히 불편함도 존재한다.<br>
사용자의 입력에 따라 데이터를 갱신하고 화면을 어떻게 업데이트해야 하는지도 코드로 작성해야 하므로 코드의 양이 많아지고 개발자도 수고로워진다.<br>
그러나 데이터의 흐름은 모두 액션이라는 한 방향으로 줄어들므로 데이터의 흐름을 추적하기 쉽고 코드를 이해하기가 한결 수월해진다.<br>

리액트는 대표적인 단방향 데이터 바인딩을 기반으로 한 라이브러리였으므로 이러한 단방향 흐름을 정의하는 Flux 패턴과 매우 궁합이 잘 맞았다.<br>
그리고 이와 동시에 이러한 Flux 패턴을 따르는 다양한 라이브러리들이 우후죽순처럼 등장하기 시작했다.<br>
상태와 그 상태의 변경에 대한 흐름과 방식을 단방향으로 채택한 것이 바로 리액트 기반의 Flux의 특징이라고 볼 수 있다.<br>

**시장 지배자 리덕스의 등장**<br>
리덕스 똫나 최초에는 이 Flux 구조를 구현하기 위해 만들어진 라이브러리 중 하나였다.<br>
이에 한 가지 더 특별한 것은 여기에 Elm 아키텍처를 도입했다는 것이다. Elm 아키텍처를 이해하려면 먼저 Elm이 무엇인지 알아야 한다.<br>
**Elm은 웹페이지를 선언적으로 작성하기 위한 언어**다. 다음은 Elm으로 HTML을 작성한 예제다.<br>

```elm
module Main exposing (..)

import Brower
import Html exposing (Html, button, div, text)
import Html.Events exposing (onClick)

-- MAIN
main =
  Browser.sandbox { init = init, update = update, view = view }

-- MODEL
type alias Model = Int

int : Model
int =
  0

-- UPDATE
type Msg
  = Increament
  | Decrement

update : Msg -> Model -> <odel
update msg model =
  case msg of
    Increment ->
      model + 1

    Decrement ->
      model - 1

-- VIEW

view : Model -> Html Msg
view model =
  div []
    [ button [ onClick Decrement ] [ text "-" ]
    , div [] [ text (String.fromInt model) ]
    , button [ onClick Increment ] [ text + "+" ]
    ]
<div>
  <button>-<button>
  <div>2</div>
  <button>+</button>
</div>
```
이게 뭐야...<br>
Elm 코드가 넟설게 보일 수 있지만 여기서 주목할 것은 model, update, view이며, 이 세가지가 바로 Elm 아키텍처의 핵심이다.
- 모델(model): 애플리케이션의 상태를 의마한다. 여기서 Model을 의미하며, 초깃값으로는 0이 주어졌다.
- 뷰(View): 모델을 표현하는 HTML을 말한다. 여기서는 Model을 인수로 받아서 HTMl을 표현한다.
- 업데이트(update): 모델을 수정하는 방식을 말한다. Increment, Decrement를 선언해 각각의 방식이 어떻게 모델을 수정하는지 나타낸다.

즉, Elm은 Flux와 마찬가지로 데이터 흐름을 세 가지로 분류하고, 이를 단방향으로 강제해 웹 애플리케이션의 상태를 안정적으로 관리하고자 노력했다.<br>
그리고 리덕스는 이 Elm 아키텍처의 영향을 받아 작성됐다.<br>

리덕스는 하나의 상태 객체를 스토어에 저장해 두고, 이 객체를 업데이트하는 작업을 디스패치해 업데이트를 수행한다. 이러한 작업은 reducer 함수로 발생시킬 수 있는데, 이 함수의 실행은 웹 애플리케이션 상태에 대한 완전히 새로운 복사본을 반환한 다음, 애플리케이션에 이 새롭게 만들어진 상태를 전파하게 된다.

이러한 리덕스의 등장은 리액트 생티계에 많은 영향을 미치게 됐다.
**Context API와 useContext**

**훅의 탄생, 그리고 React Query와 SWR**

**Recoil, Zustand, Jotai, Valtio에 이르기까지**
