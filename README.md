# Reactfood
<img width="1635" height="874" alt="pro093603" src="https://github.com/user-attachments/assets/d7cb6535-86c0-479c-8d44-28044ee6bb38" />


<img width="93" height="43" alt="image" src="https://github.com/user-attachments/assets/63ced11e-38f3-4ae7-926b-37d9bff49c66" /> <img width="74" height="37" alt="image" src="https://github.com/user-attachments/assets/115e13b4-e50a-44ea-a2dd-c97a973099a5" />

UI/Button.jsx 커스텀 버튼 컴포넌트 
재사용성과 유연성을 고려해 설계한 커스텀 버튼 컴포넌트입니다.
textOnly, className, children, 그리고 기타 HTML 속성을 props로 받아, 다양한 디자인과 동작을 한 컴포넌트로 구현할 수 있도록 구성했습니다.

textOnly prop으로 텍스트 전용 스타일 적용 가능

className을 통해 사용자 지정 스타일 동적으로 적용

children을 활용해 내부 콘텐츠(텍스트, 아이콘 등) 자유롭게 구성

...props를 통해 onClick, type, disabled 등 기본 버튼 속성 지원

해당 컴포넌트를 통해 프로젝트 전반에서 일관된 버튼 UI를 유지하면서, 필요에 따라 다양한 스타일을 간편하게 적용할 수 있도록 했습니다.

🔍 주요 부분별 설명
1. CartContext 생성
js
복사
편집
const CartContext = createContext({
  items: [],
  addItem: (item) => {},
  removeItem: (id) => {},
  clearCart: () => {},
});
Context 기본값 정의 (초기 items와 API 모양만 명시해 둠)

실제 로직은 Provider에서 구현됨

2. cartReducer – 상태 업데이트 로직
js
복사
편집
function cartReducer(state, action) {
  if (action.type === 'ADD_ITEM') { ... }
  if (action.type === 'REMOVE_ITEM') { ... }
  if (action.type === 'CLEAR_CART') { ... }
  return state;
}
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

3. CartContextProvider – 상태 공급자
js
복사
편집
export function CartContextProvider({ children }) {
  const [cart, dispatchCartAction] = useReducer(cartReducer, { items: [] });
useReducer로 상태 관리 시작

cart: 현재 상태

dispatchCartAction: 상태를 업데이트하는 함수

4. addItem, removeItem, clearCart
js
복사
편집
function addItem(item) {
  dispatchCartAction({ type: 'ADD_ITEM', item });
}
이 함수들을 통해 외부 컴포넌트가 reducer를 직접 건드리지 않고 간접적으로 상태를 바꿀 수 있음

5. Context 값 전달
js
복사
편집
<CartContext.Provider value={cartContext}>{children}</CartContext.Provider>
cartContext 객체로 하위 컴포넌트에 상태와 함수들 제공

예: useContext(CartContext)로 받아서 사용 가능

💡 실제 사용 예시 (다른 컴포넌트에서)
jsx
복사
편집
import { useContext } from 'react';
import CartContext from './path/to/CartContext';

function ProductItem({ product }) {
  const cartCtx = useContext(CartContext);

  function handleAddToCart() {
    cartCtx.addItem(product);
  }

  return (
    <button onClick={handleAddToCart}>장바구니에 추가</button>
  );
}
✅ 요약
이 구조는 Redux보다 간단하게 React에서 전역 상태를 관리하는 패턴입니다:

Context: 상태 공유

Reducer: 상태 변경 규칙

Provider: 둘을 연결해서 외부에서 쉽게 사용할 수 있게 해줌

필요하면 이 구조를 로그인 상태 관리, 모달 창 열림/닫힘, UI 테마 등에도 동일하게 응용할 수 있어요.
더 응용 예제나 개선 포인트가 필요하다면 알려줘!

장바구니 상태 관리 기능 (React Context + useReducer)
useReducer와 Context API를 조합하여 전역 상태 관리 기능을 직접 구현했습니다.
장바구니 항목 추가, 수량 조절, 삭제, 초기화 등의 액션을 하나의 reducer로 처리하고,
전역 CartContext를 통해 여러 컴포넌트에서 상태를 공유할 수 있도록 구성했습니다.

useReducer를 활용한 복잡한 상태 관리 (아이템 중복 시 수량 증가 등)

dispatch 패턴을 통해 명확하고 예측 가능한 상태 전이 설계

createContext와 Context.Provider로 전역 접근 가능한 상태 관리

성능 최적화를 고려하여 불필요한 리렌더링 방지 구조 설계
