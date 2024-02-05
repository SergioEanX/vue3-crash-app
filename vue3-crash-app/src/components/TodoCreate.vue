<script setup lang="ts">
import { reactive } from 'vue'
import TodoButton from '@/components/TodoButton.vue'

interface TodoType {
  todo: string;
  invalid:boolean|null;
  errMsg:string
}
//
// // Use reactive for the todoState object
// const todoState = reactive<TodoType>({
//   todo: "Testing",
// });


// Use a ref for a single string value
const todoState = reactive<TodoType>({
  todo:"",
  invalid:null,
  errMsg:"",
});
const emit = defineEmits(["create-todo"])
const createTodo=()=>{
  todoState.invalid=null
  if (todoState.todo!==""){

 emit("create-todo", todoState.todo)
    todoState.todo=""
    return;
  }
  todoState.invalid=true
  todoState.errMsg="todo value cannot be empty"
}

// console.log(todoState.value)


</script>

<template>
  <div class="input-wrap" :class="{'input-err':todoState.invalid}">
    <input type="text" v-model="todoState.todo" @keyup.enter="createTodo()">
    <todo-button @click="createTodo()"  />
  </div>
  <p v-show="todoState.invalid" class="err-msg">{{todoState.errMsg}}</p>

</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
    0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }


}

.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>