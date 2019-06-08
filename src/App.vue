<template>
  <div id="app">
    <section class="todoapp">
      <Header @addTodo="addTodo"/>
      <Body :todos="todos"/>
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
    }
  }
};
</script>

<style>
</style>
