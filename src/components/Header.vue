<template>
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="text"
      class="new-todo"
      autofocus
      autocomplete="off"
      placeholder="What needs to be done?"
      @keypress="handleInput"
    >
    <!-- input과   return{text: "" }를-->
    <!-- {{ text }} -->
  </header>
</template>

<script>
export default {
  data() {
    return {
      text: ""
    };
  },
  methods: {
    handleInput (event) {
      if (event.keyCode === 13) {
        if (!this.text) return; //공백일떄는 엔터를 쳐도 아무것도 안나오게

        this.$emit("addTodo", this.text);
        this.text = ""; //입력을 한 후, 공백으로 바꾸기
      };
    }
  }
};
</script>

<style>
h1 {
  position: absolute;
  top: -155px;
  width: 100%;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}
</style>
