<template>
  <ul class="todo-list">
    <AppTodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
    ></AppTodoItem>
  </ul>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import AppTodoItem from "@/components/AppTodoItem.vue";
import { Todo } from "@/types/Todo";

export default defineComponent({
  name: "AppTodoList",
  components: {
    AppTodoItem
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit('toggleTodo', id);
    },
    removeTodo(id: number) {
      this.$emit('removeTodo', id);
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id)
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>
    }
  }
})
</script>

<style scoped>

</style>