<template>
  <div class="flex justify-center items-baseline h-full pt-4 sm:p-16">
    <div class="w-[30rem] h-full m-4 flex flex-col">
      <div class="w-full mb-12 flex justify-between items-center">
          <div>
              <h1 class="text-sm sm:text-2xl font-bold inline-block text-gray-400 ml-6">To Do List</h1>
          </div>
      </div>
      <p class="w-full flex flex-row mb-5">
        <input v-model="newTask" class="basis-3/4 bg-transparent border-0 border-b-2 rounded-none p-3 focus:outline-none border-b-slate-900 text-gray-400 placeholder:ttext-gray-400 shadow-2xl" placeholder="Add a new task"/>
        <button @click="addTodo" class="ml-4 border-none p-4 px-6 shadow-2xl basis-1/4 bg-slate-900 text-gray-400 hover:text-gray-400 rounded-r-lg">Add</button>
      </p>
      <div v-for="(todo, n) in todoList" :key="todo" class="h-full">
        
        <div v-if="editing === n">
          <EditForm :todo="todo" :saveEdit="saveEdit" />
        </div>
        <div v-else>
          <Todo :todo="todo" :index="n" :is_done="is_done" :editTodo="editTodo" :removeTodo="removeTodo" :completeTodo="completeTodo"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './Todo.vue'
import EditForm from './EditForm.vue';
export default {
  name: 'TodoList',
  components: {
    Todo,
    EditForm
},
  data() {
    return {
      todoList: [],
      newTask: null,
      editing: null,
    }
  },
  mounted() {
    if (localStorage.getItem('todoList')) {
      try {
        this.todoList = JSON.parse(localStorage.getItem('todoList'));
      } catch(e) {
        localStorage.removeItem('todoList');
      }
    }
  },
  methods: {
    addTodo() {
      if (!this.newTask) {
        return;
      }
      this.todoList.push({task: this.newTask, is_done: false});
      this.newTask = '';
      this.saveTodo();
    },
    editTodo(index) {
      this.editing = index
    },
    saveEdit(todo, n) {
      const index = this.todoList.map(obj => obj.task).indexOf(n.task);
      if (!todo) {
        return;
      }

      if (index !== -1) {
          this.todoList[index].task = todo;
          this.editing = null
          this.saveTodo();
      }
    },
    completeTodo(index) {
      this.todoList[index].is_done = !this.todoList[index].is_done
    },
    removeTodo(index) {
      this.todoList.splice(index, 1);
      this.saveTodo();
    },
    saveTodo() {
      const parsed = JSON.stringify(this.todoList);
      this.editing = false
      localStorage.setItem('todoList', parsed);
    }
  },
}
</script>

<style></style>
