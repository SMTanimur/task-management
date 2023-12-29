<template>
  <div class="flex justify-center w-full">
    <div class="max-w-lg w-full p-6 flex flex-col justify-center items-center">
      <AppHeader />
      <AppFilters :activeFilter="activeFilter" @set-filter="setFilter" />
      <main class="w-full grid gap-6 mt-10">
        <AppTodoList
          :todos="filteredTodos"
          @toggle-todo="toggleTodo"
          @remove-todo="removeTodo" />
        <AppAddTodo @add-todo="addTodo" />
      </main>

      <AppFooter :stats="stats" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import AppHeader from './components/AppHeader.vue';
import AppFilters from './components/AppFilters.vue';
import AppTodoList from './components/AppTodoList.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter, {type Stats } from './components/AppFooter.vue';
import {type Todo } from './types/Todo';
import {type Filter } from './types/Filter';

interface State {
  todos: Todo[];
  activeFilter: Filter;
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter,
  },
  data(): State {
    return {
      todos: [
        { id: 1, text: 'Learn the basics of Vue', completed: true },
        { id: 2, text: 'Learn the basics of TypeScript', completed: false },
      ],
      activeFilter: 'All',
    };
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos;
        case 'Done':
          return this.doneTodos;
        case 'All':
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      };
    },
    doneTodos(): Todo[] {
      return this.todos.filter((todo) => todo.completed);
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo) => !todo.completed);
    },
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos = [...this.todos, todo];
    },
    toggleTodo(id: number) {
      this.todos.forEach((todo: Todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
      });
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    },
  },
});
</script>


