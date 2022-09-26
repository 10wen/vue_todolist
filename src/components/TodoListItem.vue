<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
      <span v-show="!todo.isEdit">{{todo.title}}</span>
      <input 
				type="text" 
        class="inputTitle"
				v-show="todo.isEdit" 
				:value="todo.title" 
				@blur="handleBlur(todo,$event)"
        @keyup.enter="handleBlur(todo,$event)"
				ref="inputTitle"
			>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button v-show="!todo.isEdit" class="btn btn-edit" @click="handleUpdate(todo)">编辑</button>
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
    },
    handleUpdate(todo){
      if (todo.hasOwnProperty('isEdit')) {
        todo.isEdit = true
      } else {
        this.$set(todo, 'isEdit', true)
      }
      this.$nextTick(()=>{
        this.$refs.inputTitle.focus()
      })
    },
    handleBlur(todo,e) {
      todo.isEdit = false
      if (!e.target.value.trim())  return alert('输入不能为空')
      this.$bus.$emit('updateTodo', todo.id, e.target.value)
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
  float: left;
  cursor: pointer;
}

li label input {
  vertical-align: middle;
  margin-right: 10px;
  position: relative;
  top: -1px;
}

.inputTitle {
  outline: none;
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
