---
title: 02. React 프로퍼티와 상태
date: 2018-04-20 19:28:10
categories:
    - React
---

앞서 컴포넌트를 만드는 방법으로

- createClass
- React Component Class
- 함수형 컴포넌트

세가지 유형의 컴포넌트에 대해서 알아봤다. 이번에도 세가지 유형의 프로퍼티와 상태를 어떻게 관리하는지 알아보자

## 프로퍼티 검증

- createClass

````jsx
import { createClass } from 'react'

const Inventory = createClass({
    displayName : "Summary",
    // 타입 검증
    propTypes: {
        id: PropTypes.number,
        name: PropTypes.string,
       	items: // 아래에서 다루겠다.
    }
    // 디폴트값
    getDefaultProps() {
        return {
			id: 0,
    		name: '',
    		items : []
        }
	}
    ...
})
````

- ES6 클래스

````jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Inventory extends Component {
    const {id, name, items} = this.props // 전개 연산자로 변수를 할당해줄 수 있다.

    static propTypes = {
        id: PropTypes.number,
        name: PropTypes.string,
        items : (props, propName) =>
            (typeof props[propName] !== 'string') ?
                new Error('문자열이어야 해용')
                (props[propName].length > 20) ?
                    new Error('20자 이내어야 함.') : null
    }
        
    static defaultProps = {
        id: 0,
        name: '',
        items: []  
    }

    render() {
        return (
            <div>
                {items.map((item, i) => 
                    <span key={i}>{item}</span>        
                )}
            </div>
        );
    }
}

// static 변수를 사용하지 않는다면
Inventory.propTypes = {
    ...
};
    
Inventory.defaultProps = {
}

export default Inventory;
````

- 함수형 컴포넌트

프로퍼티 검증 및 기본값 셋팅 방법은 클래스와 동일하게 처리해도 되고, 디폴트 인자를 지정해도 된다.

````jsx
const Inventory = ({id = 0, name = '', items = []}) => {
    return <div>
    	...
    </div>
}

Inventory.propTypes = {
    ...
}
export default Inventory;
````

## 참조(ref)

엘리먼트와 함수와 상호작용을 해야할 경우 사용된다 

- ES6 클래스

````jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Inventory extends Component {
    constructor(props) {
		super(props)
        this.submit = this.submit.bind(this)
    }
    
    submit(e) {
        const { _title } = this.refs; // 이렇게 받아올 수 있다.
        e.preventDefault();
        _title = '';
        _title.focus();
    }

    render() {
        return (
            <form onSubmit={this.submit}>
            	<input ref="_title" /> {/* 이렇게 정의해준다! */}
                <button>추가</button>
            </form>>
        );
    }
}

````

constructor가 추가됐다. 함수에서 this를 사용하려면 constructor를 재정의해서 `메서드에 this를 바인딩`해줘야 한다.  constructor를 재정의 해줬으므로 props 역시 Component의 생성자(super)를 통해서 다시 셋팅해주자.

> createClass를 이용하면 this영역을 자동으로 바인딩 해준다.

그리고 `this.refs`를 사용해서  정의한 ref값을 받아온다.

### 부모 컴포넌트로 데이터 전달

콜백을 이용하여, 부모에게 데이터를 전달해보자!

````jsx
const logInven = (title) => 
	console.log(`아이디와 이름 : ${id} ${name}`)
<Inventory onNewUser={logInven} />

...    
    submit(e) {
        const { _title } = this.refs; // 이렇게 받아올 수 있다.
        this.props.onNewUser(_title.value) // 이렇게 콜백 호출!
        _title = '';
        _title.focus();
    }

	// 콜백 함수의 디폴트값 지정해서 안정성 높이기
    static defaultProps = {
		onNewUser : f=>f // 기본 더미 함수
    }

````
- 함수형 컴포넌트

함수형 컴포넌트 안에서는 this가 없으므로 this.refs를 사용할 수 없다. 대신 함수를 사용한다. 이 함수는 input 엘리먼트 인스턴스를 인자로 받는다.

````jsx
const Inventory = ({onNewUser = f=>f}) => {
    let _title
    const submit = e => {
        e.preventDefault();
        onNewColor(_title.value)
        _title = '';
        _title.focus();
    }
    
    render (
    	<form onSubmit={submit}>
            <input ref={input => _title = input} /> {/* Input 엘리먼트를 받음 */}
            <button>추가</button>
        </form>
    )
}
````

## 상태(status)

프로퍼티(property)는 렌더링하고 나면 바뀌지 않는다! 바뀌는 데이터를 관리하기 위해서는 `status`를 사용해야한다.

- createClass

````jsx
const Dog = ({selected = true, onClick=f=>f}) =>
	<div className={(selected)? "dog selected" : "dog"}
        onClick={onClick}
    </div>
        
Dog.propTypes = {
	selected: PropTypes.bool,
    onClick: PropTypes.func
}
   
const DogHouse = createClass({
	displayName: 'DugHouse',
  getDefaultProps() {
    return {
      totalDogs: 1
    }  
  },
  // 이렇게 초기화 한다.
  getInitialState() { 
    return {
      dogsSelected: 1
    }  
  },
  change(dogsSelected) {
    this.setState({dogsSelected})
  },
        
  render() {
    const {totalDogs} = this.props
    const {dogsSelected} = this.state // props와 똑같은 방식으로 받는다.
    return (
      <div className="dog-house">
        {[...Array(totalDogs)].map((n, i) =>
            <Dog key={i}
                  selected={i<dogsSelected}
                  onClick={() => this.change(i+1)}
            />
        )}
        <p>{dogsSelected} / {totalDogs}</p>
      </div>
    )
  }
}        
````

콜백함수를 이용하여 자식에게 change함수의 결과를 돌려받아 state값을 받는다.

- ES6 클래스

````jsx
// Dog 컴포넌트 생략
...

class DogHouse extends Component {
  static propTypes = {
    totalStars: PropTypes.number
  }
  static defaultProps = {
    totalStars: 5
  }
  constructor(props) {
    // super를 호출하면 상태를 관리해주는 기능으로 인스턴스를 꾸며준다!
    super(props)
    // constructor에서 초기화 해준다!
    this.state = {
      starsSelected: 0
    }
    // 바인딩 필요
    this.change = this.change.bind(this)
  }
  change(dogsSelected) {
    this.setState({dogsSelected})
  }
  render() {
    const {totalDogs} = this.props
    const {dogsSelected} = this.state
    return (
      <div className="dog">
        {[...Array(totalDogs)].map((n, i) =>
                                    <Dog key={i}
                                      selected={i<dogsSelected}
                                      onClick={() => this.change(i+1)}
                                      />
                                   )}
        <p>{dogsSelected} / {totalDogs}</p>
      </div>
    )
  }
}
````

ES6 클래스에서는 **constructor 내부에서 state값을 초기화**해준다

### 프로퍼티로 상태 초기화 하기

입력 프로퍼티로 상태 변수를 초기화할 수 있는데, 다른 컴포넌트에서 재사용 가능한 컴포넌트를 만드는 경우이다.

- createClass

````jsx
const DogHouse = createClase({
	...
  componentWillMount() {
  	const { dogsSelected } = this.props
    if(dogSelected) {
      this.setState({dogSelected})
	  }
  }
  ...
})
````

`componentWillMount` 라는 메서드를 통해 가능하다. 컴포넌트가 마운트될때 단 한번 호출된다.

- ES6 클래스

````jsx
...
constructor(props) {
  super(props)
  this.state = {
    dogsSelected: props.dogsSelected || 0
  }
  this.change = this.change.bind(this)
}
````

명료하다!

그런데, 상태가 있는 컴포넌트의 수를 최소화하는 것이 유지보수 측면에서 좋기 때문에 이런 패턴은 최소화 하는 것이 좋다고 한다.

> 프로퍼티를 통해 상태를 초기화하기 때문에, componentWillRecevieProps 생애주기를 이용해서, 프로퍼티가 바뀔때 함께 자식 컴포넌트의 값이 바뀌도록 설정할 수 있다.

## Reference

