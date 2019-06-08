<template>
  <div id="app">
    <section class="todoapp">
      <Header @addTodo="addTodo"/>
      <Body :todos="todos" @updateDone="updateDone"/>
      <Footer/>
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
      todos: []
    };
  },
  methods:{
    addTodo (text) {
      this.todos = [
        {
          id: new Date(),
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
    }
  }
};
</script>

<style>
</style>
