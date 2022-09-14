<template>
  <div class="w-full flex flex-row mb-5">
    <input v-model="edited" class="basis-3/4 bg-transparent border-0 border-b-2 rounded-none p-3 focus:outline-none border-b-green-500 placeholder:text-gray-400 shadow-2xl" @keyup.enter="saveEdit(edited, todo)" placeholder="Write your task"/>
    <button @click="saveEdit(edited, todo)" class="ml-4 border-none p-4 px-6 shadow-2xl basis-1/4 bg-green-500 hover:bg-green-600 text-white rounded-r-lg">
      Save
    </button>
  </div>
</template>


<script>
export default {
  name: 'EditForm',
  props: {
      todo: String,
      saveEdit: Function,
  },
  data() {
    return {
      edited: this.todo.task
    }
  }
}
</script>
  