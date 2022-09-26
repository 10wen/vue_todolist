<template>
  <ul class="todo-main">
    <TodoListItem v-for="todo of todos" :key="todo.id" :todo="todo"></TodoListItem>
  </ul>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";
export default {
  name: "TodoListBody",
  props: ['todos'],
  components: { TodoListItem },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
