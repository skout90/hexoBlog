---
title: 01. 리액트 컴포넌트를 생성하는 4가지 방법
date: 2018-04-20 19:28:10
categories:
    - React
---

리액트에서 컴포넌트를 구성하는 방법에는 다양한 방법이 있다! 한번 정리해볼까?

우선 기본 엘리먼트를 만드는 방법부터 알아보자.

## 리액트 엘리먼트

````javascript
import React from 'react'

const items = [
    "울랄라",
    "후앙후앙"
]

React.createElement(
	"ul",
    {id: 1, name: "hihi", className: "hoho"}, // 프로퍼티들이 객체로 들어감
    items.map((e, i) => 
    	React.createElement("li", { key: i }, e)
    )
)
````

리액트는 `props.children` 을 사용해서 자식 엘리먼트를 렌더링한다. 

- 결과

````html
<ul id="1" name="hihi" class="hoho">
    <li>울랄라</li>
    <li>후앙후앙</li>
</ul>

{
	"type": "ul",
	"props" : {
		"id" : "1",
		"name" : "hihi",
		"className": "hoho",
		"children": [
			{"type": "li", "props": { "children": "울랄라"}},
			{"type": "li", "props": { "children": "후앙후앙"}},
		]
	}
}
````



### 리액트 컴포넌트

#### React.createClass

````javascript
import React from 'react'
import ReactDOM from 'react-dom'

const items = [
    "울랄라",
    "후앙후앙"
]

const LalaList = React.createClass({
    displayName: "LalaList",
    
    render() {
        return React.createElement(
            "ul",
            {id: 1, name: "hihi", className: "hoho"}, // 프로퍼티들이 객체로 들어감
            items.map((e, i) => 
                React.createElement("li", { key: i }, e)
            )
        )
    }
})

ReactDOM.render(
	React.createElement(LalaList, {items}, null),
    document.getElementById('react-container')
)
````

>  createClass는 사용하지 않는 추세라고 한다.

> ReactDOM.render`는 현재 DOM을 그대로 두고 갱신이 필요한 DOM 엘리먼트만 변경한다.

#### React.Component

React.Component를 상속받으면 더 간결하게 컴포넌트를 만들 수 있다.

````javascript
import React from 'react'

class LalaList extends React.Component {
    renderListItem(e, i) {
    	return React.createElement("li", {key: i}, e)
    }
    
    render() {
        return React.createElement("ul", {className: "ingredients"},
            this.props.items.map(this.renderListItem);                           
        )
    }
}
````

#### 함수형 컴포넌트

함수라서, this가 없다. 상태에 영향을 받지 않으므로 함수형 컴포넌트를 많이 활용할 수록 버그가 없는 코드를 작성할 수 있다! 

````javascript
import ReactDOM from 'react-dom'

const items = [
    "울랄라",
    "후앙후앙"
]

const LalaList = props =>  // const LalaList = ({items}) DOM의 엘리먼트들을 구조분해 가능!
	React.createElement(
        "ul",
        {id: 1, name: "hihi", className: "hoho"}, // 프로퍼티들이 객체로 들어감
        props.items.map((e, i) => 
            React.createElement("li", { key: i }, e)
        )
    )

ReactDOM.render(
	LalaList({items}), // props 값은 객체이므로 객체로 감싸 넘겨준다.
    document.getElementById('react-container')
)
````



### JSX를 사용한 컴포넌트

JSX를 사용하면, createElement 사용없이, 일반적으로 html을 작성하는 방식으로 코드를 작성할 수 있다. 하지만 브라우저는 jsx를 읽을 수 없으므로 babel을 사용해서, jsx문법들을 js처럼 바꿔서 사용한다. **굳이 확장자에 jsx를 안써도 괜찮다.** js 파일에 jsx를 작성하고 babel 설정에서 js도 읽어 들여 변환하면 된다.

> 바벨 프리셋은 babel-preset-react를 사용 : JSX를 React.createElement 호출로 변경해준다.

````jsx
// JSX를 사용하지 않을 경우 
React.createElement('div', {className:”testDivider"}, “test text", React.createElement('hr') );

// JSX를 사용할 경우
<div className=“testDivider”>test text</div>
````

````jsx
const data = [
    {
        name: 'junho',
        items: [
            { bag: 'diamond' },
            { bag: 'people' }
        ]
    },
    {
        name: 'sangja',
        items: [
            { bag: 'niche' },
            { bag: 'clever' }
        ]
    }
]

const Item = ({ name, items }) => 
	<section id={name.toLowerCase().replace(/ /g, "-")}>
        <ul className="instructions">
    		{items.map((e, i) =>
            	<li key={i}>{e.bag}</li>
            )}
    	</ul>
    </section>

const Inventory = ({ title, invens }) => 
	<div>
    	<span>{title}</span>	
    	<div>
    		{invens.map((inven, i) => 
                <Item key={i} {...inven} />           
            )}
    	</div>
	</div>

ReactDOM.render(
	<Inventory title="멍청" invens={data} />,
    document.getElementById("react-container")
)
````

루트가 되는(Inventory) 컴포넌트만 `ReactDOM.render` 해주면 나머지 컴포넌트도 함께 렌더된다.



## Reference

러닝 리액트 - 알렉스 뱅크스, 이브포셀 지음 오현석 옮김

http://inforwithme.tistory.com/entry/ReactJsJSX란