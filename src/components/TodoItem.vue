<template>
  <li>
    <label>
      <input type="checkbox" :checked="todoObj.done" @change="handleCheck(todoObj.id)"/>
      <span>{{todoObj.title}}</span>
    </label>
    <button @click="handleDelete(todoObj.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props:['todoObj'],
  methods:{
    handleCheck(id){
      
      this.$bus.$emit('checkTodo',id)
        // this.checkTodo(id)
        
    },
    handleDelete(id){
        if(!confirm('确认删除吗？')) return
        this.$bus.$emit('deleteTodo',id)
        // this.deleteTodo(id)
    }

  }
};
</script>

<style>
li button{
    display: none;
}
li:hover button{
    display: block;
}
</style>