---
title: v-model 사용하는 커스텀 컴포넌트 만들기
date: 2018-01-21 19:28:10
categories:
    - Vue
---

### input 컴포넌트

- 아래 처럼, v-model을 커스텀 컴포넌트에 사용하고 싶다! 그리고 객체를 넘기고 싶다!

````vue
<template>
  <div class="wrapper">
    <date-picker v-model="date"></date-picker>
    <p>
      Month: {{date.month}}
      Year: {{date.year}}
    </p>
  </div>
</template>

<script>
import DatePicker from './DatePicker.vue';

export default {
  components: {
    DatePicker
  },

  data() {
    return {
      date: {
        month: 1,
        year: 2017
      }
    }
  }
})
</script>
````

- 아래와 같이 선언하면 도니다.

@input 태그를 이용해서, 부모컴포넌트에게 값을 넘겨 주는 것이다.

$emit('input', 인자)를 활용하면, 값을 넘겨 줄 수 있다.

````vue
// 선언
<template>
  <div class="date-picker">
    Month: <input type="number" ref="monthPicker" :value="value.month" @input="updateDate()"/>
    Year: <input type="number" ref="yearPicker" :value="value.year" @input="updateDate()"/>
  </div>
</template>

<script>
export default {
  props: ['value'],

  methods: {
    updateDate() {
      this.$emit('input', {
        month: +this.$refs.monthPicker.value,
        year: +this.$refs.yearPicker.value
      })
    }
  }
};
</script>
````

### select 컴포넌트

- 아래와 같이 사용하고 싶다!

````vue
<custom-selectbox :items="startTimes"
                  v-model="schedule.$services[0].start">
</custom-selectbox>
````

- 이번에는 @change를 이용하고, $emit('input', 인자)를 이용한다

````vue
<template>
  <div class="custom-selectbox-container">
    <select :value="value" @change="onChange($event.target.value)">
      <option v-for="item in items" :value="item.label">
        {{item.value}}{{unit}}
      </option>
    </select>
  </div>
</template>

<script>
  export default {
    data() {
      return {
      }
    },

    methods: {
      onChange: function(value) {
        if (value === '') {
          value = null;
        }
        this.$emit('input', value);
      }
    },

    props: ['items', 'value', 'unit']
  }
</script>
````





## Reference

https://alligator.io/vuejs/add-v-model-support/

https://jsfiddle.net/dux6q43p/1/