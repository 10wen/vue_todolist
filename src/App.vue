<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <!-- <TodoListHeader :addTodo="addTodo"></TodoListHeader> -->
        <!-- 给子组件绑定自定义事件 -->
        <TodoListHeader @addTodo="addTodo"></TodoListHeader>
        <TodoListBody :todos="todos"></TodoListBody>
        <TodoListFooter 
          :todos="todos"
          @checkAllTodo="checkAllTodo" 
          @clearAllTodo="clearAllTodo"
        ></TodoListFooter>
      </div>
    </div>
  </div>
</template>

<script>
import TodoListHeader from "./components/TodoListHeader.vue";
import TodoListBody from "./components/TodoListBody.vue";
import TodoListFooter from "./components/TodoListFooter.vue";

export default {
  name: "App",
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || []
    };
  },
  methods: {
    // 添加 todo
    addTodo(item){
      this.todos.unshift(item);
    },
    //勾选or取消勾选一个todo
    checkTodo(id){
      this.todos.forEach(item => {
        if (id === item.id) item.done = !item.done;
      })
    },
    //删除一个todo
    deleteTodo(id){
      this.todos = this.todos.filter(item => item.id !== id)
    },
    //全选or取消全选
    checkAllTodo(done){
      this.todos.forEach(item => {
        item.done = done;
      })
    },
    //清除所有已经完成的todo
    clearAllTodo(){
      this.todos = this.todos.filter(item => !item.done)
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(newVal) {
        localStorage.setItem('todos', JSON.stringify(newVal))
      }
    }
  },
  mounted(){
    this.$bus.$on('checkTodo', this.checkTodo)
    this.$bus.$on('deleteTodo', this.deleteTodo)
  },
  beforeDestroy(){
    this.$bus.off('checkTodo')
    this.$bus.off('deleteTodo')
  },
  components: {
    TodoListHeader,
    TodoListBody,
    TodoListFooter,
  },
};
</script>

<style>
/* base */
body {
  background-color: #fff;
}

ul {
  padding: 0;
  list-style-type: none;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
