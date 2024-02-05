<script setup lang="ts">
import TodoCreate from '@/components/TodoCreate.vue'
import { Icon } from "@iconify/vue";
import { uid } from 'uid'

import { ref } from 'vue'
import TodoItem from '@/components/TodoItem.vue'


type Todo = {
  id:string;
  todo: string;
  isCompleted: boolean|null; // Check for this property
  isEditing: boolean|null;
};


const todoList =ref<Todo[]>([]);
const createTodo =(todo:string)=>{
  const item:Todo={
    id: uid(),
    todo,
    isCompleted:null,
    isEditing:null
  }
  todoList.value.push(item)
}

const toggleTodoComplete = (todoPos:number)=>{

todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;

}

const toggleEditTodo =(todoPos:number) =>{
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;

}

const updateTodo = (todoVal:string,todoPos:number) =>{
todoList.value[todoPos].todo=todoVal

}
</script>

<template>
  <main>
<h1>
  Create Todo
</h1>
    <todo-create @create-todo="createTodo">
    </todo-create>
    <ul class="todo-list" v-if="todoList.length>0">
      <todo-item v-for="(item, index) in todoList" :todo="item"
                 :index="index"
                 @toggle-complete="toggleTodoComplete"
                 @update-todo="updateTodo"
      @edit-todo="toggleEditTodo"/>
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" />

      <span>
        You have no todo's to complete! Add one.
      </span>
    </p>
  </main>
</template>
<style lang="scss" scoped>
main{
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin:0 auto;
  padding: 40px 16px;
  h1{
    margin-bottom: 16px;
    text-align: center;
  }
}

</style>
