<template>
    <ul class="todo-main">
        <Myitem v-for="(todo,index) in todos" :key="todo.id" :todo="todo" :delateTodo='delateTodo' :index=index  :updateTodo='updateTodo'/>
    </ul>
</template>
<script lang="ts">
import {defineComponent} from 'vue'
import Myitem from '@/components/Myitem.vue'
export default defineComponent({
  components: { Myitem },
  props:['todos','delateTodo','updateTodo'],
name:'MyList',
    
})
</script>

<style scoped>
.todo-main{
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
}
.todo-empty{
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    padding-left: 2px;
    margin-top: 10px;
}
</style>>
    