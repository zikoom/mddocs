react-redux
=================


## 1. redux를 사용하는 이유

### 1.1 redux(상태관리 라이브러리)를 사용하지 않았을때 생기는 절망 적인 상황...
react는 props를 통해 하위 컴포넌트로 값을 전달한다. 중첩된 하위 컴포넌트가 많을수록 값 전달이 어려워짐. (props -> props -> props ...)

### 1.2 절망적인 상황을 해결!! 해주는 redux

redux는 props를 통하지 않고 데이터가 필요한 컴포넌트에 직접 전달 가능 -> props 지옥에서 탈출~

## 2. readt-redux의 구성요소와 역할

- store
- action
- dispatch
