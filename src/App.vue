<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput @addTodoItem="addOneItem"></TodoInput> <!-- addTodoItem에 담긴 데이터를 addOneItem에 파라미터로 보냄 -->
    <TodoList :propsdata="todoItem"></TodoList> <!-- todoItem 데이터를 propsdata에 담아 TodoList.vue로 보냄 -->
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      todoItem:[]
    }
  },
  methods: {
    addOneItem(todoItem) { //리스트 추가 기능
      //저장하는 로직
      var obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItem.push(obj);
    }
  },
  created() {
    // TodoList 기능 가져옴
    if(localStorage.length > 0) {
      for(var i = 0; i<localStorage.length; i++) {
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItem.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          // this.todoItem.push(localStorage.key(i));
        }
      }
    }
  },
  components: {
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F6;
  }

  input {
    border-style: groove;
    width: 80%;
    height: 89%;
  }

  button {
    border-style: groove;
  }

  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
