<template>
  <!-- TOOD better ui and css -->
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <h2 class="text-xl font-bold">TodoList</h2>
      <p class="flex mt-4">
        <input v-model="newTask" class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker" placeholder="Add Todo"/>
        <button @click="addTodo"  class="btn ml-4 border-none p-4 px-6 shadow-2xl">Add</button>
      </p>
      <div v-for="(todo, n) in todoList" :key="todo">
        
        <div v-if="editing === n">
          <EditForm :todo="todo" :saveEdit="saveEdit" />
        </div>
        <div v-else>
          <AddForm :todo="todo" :index="n" :is_done="is_done" :editTodo="editTodo" :removeTodo="removeTodo" :completeTodo="completeTodo"/>
        </div>
      </div>
    </div>
</template>

<script>
import AddForm from './AddForm.vue'
import EditForm from './EditForm.vue';
export default {
  name: 'TodoList',
  // props: {
  //   todo: String,
  // },
  components: {
    AddForm,
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.edit {
  display: inline-flex;
  align-items: center;
}
.todo {
  flex-direction: column;
}
</style>
