<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入代办事项" @keyup.enter="addTodoObj"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: "TodoHeader",
  methods:{
    addTodoObj(e){
      if(!e.target.value.trim()){
        alert('数据不能为空')
        return
      }
      const todoObj = {
        id:nanoid(),
        title:e.target.value,
        done:false
      }
      this.$emit('add',todoObj)
      e.target.value = ''
    }
  },
};
</script>

<style>
</style>