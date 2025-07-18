# Reactfood
Reactfood 프로젝트에서는 React를 기반으로 한 컴포넌트 중심 설계를 통해 사용자 인터페이스를 개발했습니다. 장바구니와 결제 상태와 같은 전역 상태 관리를 위해 Context API와 useReducer를 활용하여, 복잡한 상태 전이와 데이터 흐름을 구조적으로 처리했습니다.

모달과 같은 UI 요소는 createPortal을 통해 별도의 DOM 위치에 렌더링함으로써 깔끔하고 직관적인 사용자 경험을 제공하였고, useRef와 useEffect를 이용해 DOM 제어 및 생명 주기 관리를 효과적으로 수행했습니다.

또한, 주문 데이터를 서버로 전송할 때는 useActionState를 활용하여 폼 제출 상태를 관리했고, 커스텀 훅인 useHttp를 만들어 HTTP 요청 처리 로직을 재사용 가능하게 분리하여 네트워크 통신 흐름의 일관성과 유지보수성을 높였습니다.

<img width="1635" height="874" alt="pro093603" src="https://github.com/user-attachments/assets/d7cb6535-86c0-479c-8d44-28044ee6bb38" />


## UI/Button.jsx 커스텀 버튼 컴포넌트
<img width="93" height="43" alt="image" src="https://github.com/user-attachments/assets/63ced11e-38f3-4ae7-926b-37d9bff49c66" /> <img width="74" height="37" alt="image" src="https://github.com/user-attachments/assets/115e13b4-e50a-44ea-a2dd-c97a973099a5" />

재사용성과 유연성을 고려해 설계한 **커스텀 버튼 컴포넌트**입니다.
textOnly, className, children, 그리고 기타 HTML 속성을 props로 받아, 다양한 디자인과 동작을 한 컴포넌트로 구현할 수 있도록 구성했습니다.

textOnly prop으로 텍스트 전용 스타일 적용 가능

className을 통해 사용자 지정 스타일 동적으로 적용

children을 활용해 내부 콘텐츠(텍스트, 아이콘 등) 자유롭게 구성

...props를 통해 onClick, type, disabled 등 기본 버튼 속성 지원

해당 컴포넌트를 통해 프로젝트 전반에서 일관된 버튼 UI를 유지하면서, 필요에 따라 다양한 스타일을 간편하게 적용할 수 있도록 했습니다.

## 장바구니 상태 관리 기능 (React Context + useReducer)

<img width="1567" height="835" alt="image" src="https://github.com/user-attachments/assets/b6e2be95-3c43-46cc-934f-a7e8c99358dd" />

### 1. CartContext 생성 ###

### 2. CartReducer – 상태 업데이트 로직 ###

state: 현재 장바구니 상태
action: 어떤 행동을 할지 명시 (type과 함께 필요한 payload도 전달됨)

✅ ADD_ITEM 로직
이미 있는 아이템이면 quantity 증가
없으면 새로 추가

✅ REMOVE_ITEM 로직
quantity가 1이면 삭제
그 이상이면 quantity 감소

✅ CLEAR_CART
아이템 배열을 초기화

### 3. CartContextProvider – 상태 공급자 ###

cart: 현재 상태

dispatchCartAction: 상태를 업데이트하는 함수

### 4. addItem, removeItem, clearCart ###

이 함수들을 통해 외부 컴포넌트가 reducer를 직접 건드리지 않고 간접적으로 상태를 바꿀 수 있음

### 5. Context 값 전달 ###

cartContext 객체로 하위 컴포넌트에 상태와 함수들 제공

### ✅ 요약 ###

Context: 상태 공유

Reducer: 상태 변경 규칙

Provider: 둘을 연결해서 외부에서 쉽게 사용할 수 있게 해줌

## UI/Button.jsx 커스텀 버튼 컴포넌트
createPortal을 이용해 이 모달을 다른 DOM 위치에 렌더링합니다.

ref={dialog}: 위에서 만든 ref로 이 DOM 요소에 접근합니다.

onClose={onClose}: 모달이 닫힐 때 콜백 함수 실행.

## UserProgressContext – 전역 상태 관리 (React Context API)

<img width="1550" height="814" alt="image" src="https://github.com/user-attachments/assets/0f1716bc-9b2c-4911-84b1-06b6d4c3b98f" />

### React의 Context API를 사용해 장바구니(cart) 및 결제(checkout) 진행 상태를 전역에서 관리하는 로직을 구현했습니다. 각 상태 전환 함수를 함께 제공함으로써 컴포넌트 간 복잡한 props 전달 없이 UI 흐름 제어가 가능합니다.

progress 상태를 통해 'cart', 'checkout', ''(초기 상태) 중 현재 화면을 구분

showCart(), showCheckout() 함수로 해당 화면 상태 진입

hideCart(), hideCheckout() 함수로 상태 초기화 및 종료 처리

전역 상태로 관리하여 다수의 컴포넌트에서 접근 가능

### 장바구니와 결제 상태를 다루는 함수들
showCart() → 상태를 'cart'로 바꿔서 장바구니를 보여줍니다.

hideCart() → 상태를 초기화 ('')해서 장바구니를 숨깁니다.

showCheckout() → 상태를 'checkout'으로 바꿔서 결제 화면을 보여줍니다.

hideCheckout() → 상태를 초기화해서 결제 화면을 숨깁니다.

## CheckoutForm
<img width="1694" height="863" alt="image" src="https://github.com/user-attachments/assets/aaed7cc0-597a-4c51-b44a-855df7a47a2e" />

 Checkout 컴포넌트는 React Context, 커스텀 훅(useHttp), 그리고 HTML Form과 useActionState를 통한 폼 제출 처리를 사용하는 결제(Checkout) 모달입니다.
주요 기능은: 장바구니 데이터를 보여주고, 사용자 정보를 입력받아 서버로 주문 데이터를 전송하는 것입니다.
<img width="1639" height="847" alt="image" src="https://github.com/user-attachments/assets/db9a4674-feee-4a26-873a-665853528569" />

실패시
<img width="1602" height="805" alt="image" src="https://github.com/user-attachments/assets/2345effc-6686-493e-8598-dd7d374b94d2" />


