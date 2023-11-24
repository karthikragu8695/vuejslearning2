<template>
  <h1 class="text-center font-bold text-5xl text-white mt-10">Todo List</h1>
 <emp-form></emp-form>
<todo-list></todo-list>
</template>

<script>
import TodoList from './components/TodoList.vue';
import EmpForm from './components/EmpForm.vue';

export default {
  name: 'App',
  components: {
    TodoList,
    EmpForm
  }
}
</script>
<style>
body{
  background-color: gray;
}
</style>
