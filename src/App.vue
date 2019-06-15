<template>
  <div id="app">
    <section class="todoapp">
      <Header @addTodo="addTodo"/>
      <Body :todos="filtedTodos" @updateDone="updateDone" @removeTodo="removeTodo" @updateTodo="updateTodo"/>
      <Footer :size="size" :filterType="filterType" @onChangeFilter="handelFilterType"/>
    </section>
  </div>
</template>

<script>
import "./assets/css/main.css";

import Header from "./components/Header";
import Body from "./components/Body";
import Footer from "./components/Footer";

export default {
  components: {
    Header,
    Body,
    Footer
  },
  data() {
    return{
      todos: [],
      filterType: "All"
    };
  },
  computed: {
    filtedTodos(){
      switch(this.filterType) {
        case 'All': {
          return this.todos;
        }
        case 'Active': {
          return this.todos.filter(todo => !todo.isDone);
        }
        case 'Completed': {
          return this.todos.filter(todo => !todo.isDone);
        }
        default: {
          return this.todos;
        }
      }
    },
    size () {
      return this.filtedTodos.length;
    }
  },
  methods:{
    addTodo (text) {
      this.todos = [
        {
          id: new Date().getTime(),
          text,
          isDone: false
        },
        ...this.todos
      ];
    },
    updateDone(id) { //구분할 값은 id로 받음
      const currentTodos = [...this.todos];
      const todo = currentTodos.find((todo) => todo.id ===  id) //넘겨받은 id가 있는지 찾음
      
      if (todo){ //검색된 애가 있으면 트루 없으면 펄스
        todo.isDone = !todo.isDone;
        this.todos = currentTodos;
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    updateTodo({ id, text}){
      const currentTodos = [...this.todos];
      const todo = currentTodos.find((todo) => todo.id ===  id)

      if (todo){ 
        todo.text = text;
        this.todos = currentTodos;
      }
    },
    handelFilterType(type){
      this.filterType= type;
    }
  }
};
</script>

<style>
</style>
