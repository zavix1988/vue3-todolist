<template>
  <AppHeader></AppHeader>

  <AppFilters
      :active-filter="activeFilter"
      @set-filter="setFilter"
  ></AppFilters>

    <main class="app-main">
      <AppTodoList
          :todos="filterTodos"
          @toggle-todo="toggleTodo"
          @remove-todo="removeTodo"
      ></AppTodoList>

      <AppAddTodoItem
          @add-todo="addTodo"
      ></AppAddTodoItem>
    </main>

  <AppFooter
    :stats="stats"
  ></AppFooter>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import AppHeader from "@/components/AppHeader.vue";
import AppFilters from "@/components/AppFilters.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodoItem from "@/components/AppAddTodoItem.vue"
import AppFooter, {Stats} from "@/components/AppFooter.vue"
import {Todo} from "@/types/Todo";
import {Filter} from "@/types/Filter";

interface State {
  todos: Todo[],
  activeFilter: Filter
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodoItem,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: 'Learn the basics of Vue', completed: true },
        { id: 1, text: 'Learn the basics of Typescript', completed: false },
        { id: 2, text: 'Subscribe to the channel', completed: false },
      ],
      activeFilter: 'All'
    }
  },
  computed: {
    filterTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active' : return this.activeTodos;
        case 'Done' : return this.doneTodos;
        case 'All' :
        default: return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter(todo => !todo.completed)
    },
    doneTodos(): Todo[] {
      return this.todos.filter(todo => todo.completed)
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    }
  }
})
</script>