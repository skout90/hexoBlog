---
title: element를 bottom에 위치시키는 3가지 방법
date: 2018-08-29 19:28:10
categories:
    - CSS
---

- flex

````css
.parent {
  display: flex;
  flex-direction: column;
}
.child {
  margin-top: auto;
}

/* 또는 */
.parent {
  display: flex;
}
.child {
  align-self: flex-end;
}
````

- absolute

````css
.parent {
    position: relative;
}

.child {
    position: absolute;
    bottom: 0;
}
````

- table row

````css
.parent {
    height:100%;
    border-collapse:collapse;
    display : table;
}

.child {
    display : table-row;
    vertical-align : bottom;
    height: 1px;
}
````



## Reference

https://stackoverflow.com/questions/526035/how-can-i-position-my-div-at-the-bottom-of-its-container