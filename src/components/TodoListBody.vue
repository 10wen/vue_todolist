<template>
  <ul class="todo-main">
    <transition-group name="todo" appear>
      <TodoListItem v-for="todo of todos" :key="todo.id" :todo="todo"></TodoListItem>
    </transition-group>
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

@keyframes todoItemAnimate {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0px);
  }
}

.todo-enter-active {
  animation: todoItemAnimate 0.25s linear;
}
.todo-leave-active {
  animation: todoItemAnimate 0.25s linear reverse;
}

</style>
