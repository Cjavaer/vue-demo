<template>
  <transition name="fade">
    <li class="todolist">
        <i icon="success" @click="todoComplete" v-if="complete" key="success"></i>
        <i icon="circle" @click="todoComplete" v-else key="circle"></i>
      <span class="todoitem" :class="{completed:complete}">{{todo.item}}</span>
      <i icon="e_radio" key="radio" v-if="complete"></i>
      <i icon="close" key="close" @click="deletTodoItem" v-else></i>
      <p>{{count}}</p>
    </li>
  </transition>
</template>

<script>
import { createNamespacedHelpers } from 'vuex'
const { mapState} = createNamespacedHelpers('testModuleA');

export default {
  name:'demo-todo-item',
  props:['todo'],
  inheritAttrs:true,
  data(){
    return {
      complete:false
    }
  },
  filters:{//过滤器
    upperCaseInput(value){
      if(!value) return ''
      return value.toUpperCase();
    }
  },
  computed:{
    ...mapState({
      count: state => state.count,
    })
  },
  methods:{
    deletTodoItem(){
      this.$emit('todoItemCallback')
    },
    todoComplete(e){
      this.complete = !this.complete;
    }
  }
}
</script>
<style scoped>
.todolist{
  margin: 10px;
}
.todoitem{
  margin:10px;
  color:#999;
}
.todoitem.completed{
  color:#ccc;
  text-decoration: line-through;
}
/* 过渡*/
/* .fade-enter-active, .fade-leave-active {
  transition: opacity .6s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
} */
.fade-enter-active {
  animation: bounce-in .3s;
}
.fade-leave-active {
  animation: bounce-out .3s;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
    transform: translateX(20%)
  }
  100% {
    transform: scale(1);
    transform: translateX(0)
  }
}
@keyframes bounce-out {
  0% {
   transform: translateX(0)
  }
  50%{
    transform: translateX(10%)
  }
  100% {
    transform: translateX(-100%)
  }
}
</style>


