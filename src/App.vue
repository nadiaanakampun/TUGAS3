<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
    {id: id++, text: 'test', done: true},
    {id: id++, text: 'learn vue', done: true},
    {id: id++, text: 'test lagi', done: false}
])

function tambah(){
  todos.value.push({id: id++, text: newTodo.value})
  newTodo.value=''
}

function hapus(todo){
  todos.value = todos.value.filter((t) => t !== todo)
}

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})
</script>

<template>
  <form>
    <input v-model="newTodo" placeholder="input here">
    <button @click.prevent="tambah">Tambah</button>
  </form>

  <ol>
    <li v-for="todo in filteredTodos" :key="todo.id">
    <input type="checkbox" v-model="todo.done">
    <span :class="{done: todo.done}">{{ todo.text }}</span>
    <button @click="hapus(todo)">hapus</button>
    </li>
  </ol>

  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>

