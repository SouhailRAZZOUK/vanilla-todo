<script setup>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import CreateTodoForm from './CreateTodoForm.vue'

const todos = ref([
  { id: 1, title: 'Todo 1', done: false },
  { id: 2, title: 'Todo 2', done: true },
  { id: 3, title: 'Todo 3', done: false }
])
const editedTodo = ref(null)
const handleNewTodo = (newTodo) => {
  const id = Math.max(...todos.value.map(({ id }) => id)) + 1
  todos.value.push({ id, title: newTodo, done: false })
}
const handleEditedTodoChange = (id) => (editedTodo.value = id)
const handleSaveEditedTodo = (todo) => {
  const { id: targetId } = todo
  const targetTodoIndex = todos.value.findIndex(({ id }) => id === targetId)
  todos.value[targetTodoIndex] = todo
}
</script>

<template>
  <CreateTodoForm @newTodo="handleNewTodo" />
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <TodoItem
        :todo="todo"
        :editedTodo="editedTodo"
        @showEditedTodo="handleEditedTodoChange"
        @saveEditedTodo="handleSaveEditedTodo"
      />
    </li>
  </ul>
</template>
