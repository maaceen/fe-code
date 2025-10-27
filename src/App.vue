<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader @add="add"></TodoHeader>
        <TodoMain 
        :todos="todos"
        ></TodoMain>
        <TodoFooter 
        :todos="todos"
        @checkTodoAll="checkTodoAll"
        @clearDoneTodo="clearDoneTodo"
        ></TodoFooter>
      </div>
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  name: "App",
  data(){
    return {
      todos:JSON.parse(localStorage.getItem('todos'))
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods:{
    add(todoObj){
      this.todos.unshift(todoObj)
    },
    checkTodo(id){
      
      this.todos.forEach(todo => {
        if(todo.id === id){
          todo.done = !todo.done
        }
      })
    },
    deleteTodo(id){
      
      this.todos = this.todos.filter(todo => todo.id !== id)
      
    },
    checkTodoAll(checked){
      this.todos.forEach(todo => todo.done = checked)
    },
    clearDoneTodo(){
      if(!confirm('确认清除已完成任务吗？')) return
      this.todos = this.todos.filter(todo => !todo.done)
    }
  },
  watch:{
    // todos(newTodos){
    //   localStorage.setItem('todos',JSON.stringify(newTodos))
    // }
    todos:{
      deep:true,
      handler(newTodos){
        localStorage.setItem('todos',JSON.stringify(newTodos))
      }
    }
  },
  mounted(){
    
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('deleteTodo',this.deleteTodo)
  }
};
</script>

<style>
body,
ul {
  margin: 0;
  border: 0;
  padding: 0;
}
ul {
  list-style-type: none;
}
.todo-container{
  display: flex;
  justify-content: center;
}
.todo-wrap{
  display: flex;
  flex-direction: column;
}
.todo-header input{
  width: 400px;
  height: 50px;
  margin-bottom: 30px;
}
.todo-main li{
  height: 30px;
  border-bottom: 1px solid black;
  border-left: 1px solid black;
  border-right: 1px solid black;
  border-radius: 3px;
  display: flex;
  align-items: center;
  
}
.todo-main li:first-child{
  border-top: 1px solid black;
}
.todo-footer{
  margin-top: 30px;
  display: flex;
  flex-direction: column;
}
.todo-footer .number{
  margin-bottom: 10px;
}
</style>
