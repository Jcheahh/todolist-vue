<template>
  <div class="task_animation w-full bg-slate-900 p-3 my-3 border-0 border-l-4 border-red-500 rounded-r-lg flex justify-between items-center shadow-2xl" :class="(todo.is_done) ? 'border-green-500' : ' '">
      <span @click="completeTodo(index)" class="cursor-pointer text-gray-400 overflow-hidden w-[80%] h-6 relative" :class="(todo.is_done) ? 'line-through text-gray-400 font-bold' : ' '">
        {{ todo.task }}
      </span>
      <button @click="editTodo(index)" class="text-green-500 mr-4 cursor-pointer">
        Edit
      </button>
      <button @click="removeTodo(index)" class="text-red-500 cursor-pointer">
        Remove
      </button>
    
  </div>
</template>


<script>
export default {
  name: 'Todo',
  props: {
      todo: String,
      index: Number,
      editTodo: Function,
      removeTodo: Function,
      completeTodo: Function,
  }
}
</script>

<style>
.task_animation {
  animation: task_animation .3s cubic-bezier(0, 0, 0.2, 1) forwards;
}


@keyframes task_animation {
  0% {
      transform: scale(.5);
      opacity: 0;
  }

  100% {
      transform: scale(1);
      opacity: 1;
  }
}
</style>