<template>
<li @mouseenter="mouseHandler(true)" @mouseleave='mouseHandler(false)' :style="{backgroundColor:bgColor,color:myColor}">
    <label>
        <input type="checkbox" v-model="isComptete" />
        <span>{{todo.title}}</span>
    </label>
    <button v-show="isShow" @click="delTodo" >删除</button>
</li>
</template>
<script lang="ts">
import { Todo } from '@/types/todo'
import {computed, defineComponent, ref} from 'vue'
export default defineComponent({
    name:'Myitem',
    props:{
        todo:{
            type:Object as ()=> Todo,
            required:true
            },
        delateTodo:{
            type:Function,
            required:true
        },
        index:{
            type:Number,
            requried:true
        },
        updateTodo:{
            type:Function,
            required:true
        },
    },
   setup(props){
    const bgColor = ref('white')
    const myColor = ref('black')
    const isShow = ref(false)
    const mouseHandler = (flag:Boolean) =>{
        if(flag){
            bgColor.value = 'pink'
            myColor.value = 'green'
            isShow.value = true
        }else{
            myColor.value = 'black'
            bgColor.value = 'white'
            isShow.value = false
        }
    }
    const delTodo = ()=>{
        if((window.confirm('确定删除吗!'))){
            props.delateTodo(props.index)
        }
    }
    const isComptete=computed({
        get(){
            return props.todo.isCompleted
        },
        set(val){
            props.updateTodo(props.todo,val)
        }
    })
    return{
        mouseHandler,
        bgColor,
        myColor,
        isShow,
        delTodo,
        isComptete
    }
   }
})
</script>

<style scoped>
li{
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
}
li label{
    float: left;
    cursor: pointer;
}
li label li input{
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
}
li button{
    float: right;
    /* display: none; */
    margin-top: 3px;
    color: red;
}
li:before{
    content: initial;
}
li:last-child{
    border-bottom: none;
}
</style>>
    