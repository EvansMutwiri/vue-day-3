<template>
  <div>
    <h1>To do</h1><br>

    <p v-if="myToDoList.length > 4" class="tooMuch">Too many items on your plate!!</p>

    <form v-bind:disabled="!newToDo.value" @submit.prevent="addToDo">

      <input type="text" v-model="newToDo" placeholder="Add new task" required>

    </form>
  </div>
  <div>
    <ol>
      <li v-for="(todo) in myToDoList" :key="todo.id" @click="toggleDone(todo)" :class="{ done: todo.completed }">
        {{ todo.label }}</li>
    </ol>
  </div>

</template>

<script>
import { ref } from '@vue/reactivity'
export default {
  setup() {

    const myToDoList = ref([
      { id: 1, label: 'VUE JS DAY 4 - CLASS & STYLE BINDINGS, CONDITIONAL RENDERING, LIST RENDERING', completed: true },
      { id: 2, label: 'VUE JS DAY 4 - EVENT HANDLING AND FORM INPUT BINDING', completed: false },
      { id: 3, label: 'VUEJS DAY 5 - LIFE CYCLE HOOKS, WATCHERS AND TEMPLATE REFS'}
    ]);

    const newToDo = ref("");

    const addToDo = () => {
      myToDoList.value.push({id: myToDoList.value.length + 1, label: newToDo.value, completed: false});
      newToDo.value = ""
    }

    const toggleDone = (todo) => {
      todo.completed = !todo.completed
    }

    return {
      myToDoList,
      toggleDone,
      newToDo,
      addToDo
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
  text-decoration-thickness: 2px;
  text-decoration-color: brown;
}

.tooMuch {
  color: brown;
}
</style>