<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const emits = defineEmits(['newTodo'])

const addTodo = (e) => {
  e.preventDefault()
  emits('newTodo', newTodo)
}
</script>

<template>
  <form @submit="addTodo">
    <input type="text" name="todo-title" id="todo-title" v-model="newTodo" />
    <button>Add</button>
  </form>
</template>
