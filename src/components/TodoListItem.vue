<template>
  <li>
    <label :for="todo.id" @change="handleCheck(todo.id)">
      <input type="checkbox" :id="todo.id" :checked="todo.done"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ['todo'],
  methods: {
    //勾选or取消勾选
    handleCheck(id){
      //通知App组件将对应的todo对象的done值取反
      // this.checkTodo(id)
      this.$bus.$emit('checkTodo', id)
    },
    //删除
    handleDelete(id){
      if(confirm('确定删除吗？')){
        //通知App组件将对应的todo对象删除
        // this.deleteTodo(id)
        this.$bus.$emit('deleteTodo', id)
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  width: 500px;
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>
