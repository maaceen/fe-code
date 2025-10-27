<template>
  <ul class="todo-main">
          <TodoItem 
          v-for="todoObj in todos" :key="todoObj.id" 
          :todoObj="todoObj"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
          ></TodoItem>
          
        </ul>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
  name:'TodoMain',
  components:{
    TodoItem
  },
  props:['todos','checkTodo','deleteTodo']
}
</script>

<style>

</style>