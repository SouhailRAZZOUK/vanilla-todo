<script setup>
import { ref } from 'vue'

const emits = defineEmits(['saveEditedTodo', 'showEditedTodo'])
const { todo } = defineProps({
  todo: {
    title: String,
    id: Number,
    done: Boolean
  },
  editedTodo: Number
})
const innerTodo = ref(todo)
const showEditForm = (id) => {
  emits('showEditedTodo', id)
}
const saveEditForm = (e) => {
  e.preventDefault()
  emits('saveEditedTodo', innerTodo)
  emits('showEditedTodo', null)
}
const toggleTodoStatus = () => {
  innerTodo.value.done = !innerTodo.value.done
  emits('saveEditedTodo', innerTodo)
}
</script>

<template>
  <form @submit="saveEditForm" v-show="editedTodo === innerTodo.id">
    <input type="text" v-model="innerTodo.title" />
    <input type="checkbox" :checked="innerTodo.done" @change="toggleTodoStatus" />
    <button>Save</button>
  </form>
  <div v-show="editedTodo !== innerTodo.id">
    <span @click="showEditForm(innerTodo.id)">{{ innerTodo.title }}</span>
    <input type="checkbox" :checked="innerTodo.done" @change="toggleTodoStatus" />
  </div>
</template>
