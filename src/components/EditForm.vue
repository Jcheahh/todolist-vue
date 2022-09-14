<template>
  <div class="flex row items-center justify-between w-full py-1 px-4 my-1 rounded border bg-gray-100 text-gray-600">
    <input v-model="edited" class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker" />
    <button @click="saveEdit(edited, todo)" class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purple-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2">Save</button>
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
  