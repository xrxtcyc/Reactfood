# Reactfood
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
<img width="1550" height="814" alt="image" src="https://github.com/user-attachments/assets/0f1716bc-9b2c-4911-84b1-06b6d4c3b98f" />

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

예: 모달을 <div id="modal"></div> 안에 그립니다.

<dialog>: HTML5에서 제공하는 기본 모달 요소입니다.

ref={dialog}: 위에서 만든 ref로 이 DOM 요소에 접근합니다.

onClose={onClose}: 모달이 닫힐 때 콜백 함수 실행.


