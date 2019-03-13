- actions : 
  - login 함수
    - setLoggedInState를 dispatch
      - setLoggedInState는 loggedInState를 인자로 받아서 리턴함
  - 액션 생성기
    - 위의 로그인 함수를 생성해줌
- reducers : 액션을 실행하여 - 이전값에서 새로운 값을 적용
  - loggedInStatus 



actions -> dispatch로 reducer실행 -> reducer에서 새로운 값으로 적용



사용

아래와 같이 props에 액션 생성기와 state를 연결해줌.

````javascript
const mapStateToProps = (state) => {
  return {
    loggedInStatus: state.loggedInStatus,
  }
};

const mapDispatchToProps = (dispatch) => {
  return bindActionCreators(ActionCreators, dispatch);
};

// 사용
this.props.logIn(emailAddress, password)
````

