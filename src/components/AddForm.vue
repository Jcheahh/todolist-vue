<template>
  <div class="flex row items-center justify-between w-full py-1 px-4 my-1 rounded border bg-gray-100 text-gray-600">
    <div class="items-center column">
      <input type="checkbox" @click="completeTodo(index)"/>
      <span class="ml-5 w-full text-grey-darkest" :class="(todo.is_done) ? 'line-through text-gray-400 font-bold' : ' '">{{ todo.task }}</span>
    </div>
    <div class="items-center row-reverse">

      <button @click="editTodo(index)"  class="fa-solid fa-pen-to-square text-green-500 cursor-pointer">Edit</button>
      <button @click="removeTodo(index)" class="px-4 py-1 text-sm text-red-600 font-semibold rounded-full border border-red-200 hover:text-white hover:bg-red-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-red-600 focus:ring-offset-2">Remove</button>
    </div>
    
    
  </div>
</template>


<script>
export default {
  name: 'AddForm',
  props: {
      todo: String,
      index: Number,
      editTodo: Function,
      removeTodo: Function,
      completeTodo: Function,
  }
}
</script>
