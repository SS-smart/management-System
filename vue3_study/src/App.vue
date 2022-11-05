<template>
<div class="todo-container">
  <div class="todo-warp">
    <Myhead :addTodo="addTodo" />
    <MyList :todos="todos" :delateTodo='delateTodo' :updateTodo="updateTodo"/>
    <MyFooter :todos="todos" :checkAll="checkAll" :clearAllCompletedTodos="clearAllCompletedTodos"/>
  </div>
</div>
</template>

<script lang="ts">
import { defineComponent, reactive,toRefs} from 'vue';
import Myhead from '@/components/Myhead.vue'
import MyList from '@/components/MyList.vue'
import MyFooter from '@/components/MyFooter.vue'
import {Todo} from './types/todo'
export default defineComponent({
  name: 'App',
  components:{
      Myhead,
      MyList,
      MyFooter
  },
  setup() {
    // 定义一个数组数据
    const state = reactive<{todos:Todo[]}>({
      todos:[{
        id:1,title:'明天买车',isCompleted:false
      },{
        id:2,title:'后天买房',isCompleted:true
      },{
        id:3,title:'大大后天结婚',isCompleted:false
      }],
    });
    // 添加
    const addTodo = (todo:Todo)=>{
        state.todos.unshift(todo)  
    }
    // 删除
    const delateTodo = (index:number)=>{
      state.todos.splice(index,1)
    }
    // 修改复选框
    const updateTodo = (todo:Todo,isCompleted:boolean)=>{
      todo.isCompleted = isCompleted
    }
    // 全选或者全不选操作
    const checkAll = (isCompleted:boolean)=>{
        state.todos.forEach((todo)=>{
            todo.isCompleted = isCompleted
        })
    }
    // 删除所有
    const clearAllCompletedTodos = ()=>{
      state.todos = state.todos.filter(todo=>!todo.isCompleted)
    }
    return{
      ...toRefs(state),
      addTodo,
      delateTodo,
      updateTodo,
      checkAll,
      clearAllCompletedTodos
    }
  }
});
</script>

<style scoped>
.todo-container{
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-warp{
  padding: 10px;
  border: 1px solid red;
  border-radius: 5px;
}
</style>
