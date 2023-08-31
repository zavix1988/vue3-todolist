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
import {defineComponent} from 'vue'
import AppTodoItem from "@/components/AppTodoItem.vue";
import { Todo } from "@/types/Todo";

interface State {
  todos: Todo[]
}

export default defineComponent({
  name: "AppTodoList",
  components: {
    AppTodoItem
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: 'Learn the basics of Vue', completed: true },
        { id: 1, text: 'Learn the basics of Typescript', completed: false },
        { id: 2, text: 'Subscribe to the channel', completed: false },
      ]
    }
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    }
  }
})
</script>

<style scoped>

</style>