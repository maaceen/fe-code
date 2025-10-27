<template>
  <div class="todo-footer" v-show="todoAll">
          <div class="number">
            <label>
            <!-- <input type="checkbox" :checked="isAll" @change="checkAll"> -->
            <input type="checkbox" v-model="isAll">
          </label>
          <span>已完成{{todoDone}}/全部{{todoAll}}</span>
          </div>
          
          <button @click="clearTodo">清除已完成任务</button>
        </div>
</template>

<script>
export default {
  name:'TodoFooter',
  props:['todos'],
  computed:{
    todoDone(){
      return this.todos.reduce((pre,todo) =>{
        return pre + (todo.done === true ? 1 : 0)
      },0)
      
    },
    todoAll(){
      return this.todos.length
      },
    // 改进前的代码
    // isAll(){
    //   return this.todoDone === this.todoAll && this.todoAll > 0
    // }
    // 改进后的代码
    isAll:{
      get(){
        return this.todoDone === this.todoAll && this.todoAll > 0
      },
      set(value){
        this.$emit('checkTodoAll',value)
      }
    }
  },
  methods:{
    checkAll(e){
      this.$emit('checkTodoAll',e.target.checked)
      // this.checkTodoAll(e.target.checked)
      
    },
    clearTodo(){
      this.$emit('clearDoneTodo')
      // this.clearDoneTodo()
    }
  }
}
</script>

<style>

</style>