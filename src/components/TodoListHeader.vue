<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add">
  </div>
</template>

<script>
import {nanoid} from 'nanoid';

export default {
  name: 'TodoListHeader',
  // props: ['addTodo'],
  data(){
    return {
      title: ''
    }
  },
  methods: {
    add(){
      //校验数据
			if(!this.title.trim()) return alert('输入不能为空')
      let item = {id:nanoid(), title: this.title, done: false};
      // this.addTodo(item)
      this.$emit('addTodo', item)
      this.title = ''
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* todo-header */
.todo-header input {
  width: 560px;
  height: 28px;
  border-radius: 5px;
  border: 1px solid #ddd;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}

</style>
