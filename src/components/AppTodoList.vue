<template>
    <ul class="text-lg" v-for="todo in todos" :key="todo.id">
      <AppTodoItem
        :todo="todo"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo" />
    </ul>
  </template>
  
  <script lang="ts">
  import { defineComponent, type PropType } from 'vue';
  import AppTodoItem from './AppTodoItem.vue';
  import { type Todo } from '../types/Todo';
  
  export default defineComponent({
    components: {
      AppTodoItem,
    },
    props: {
      todos: {
        type: Array as PropType<Todo[]>,
        required: true,
      },
    },
    methods: {
      toggleTodo(id: number) {
        this.$emit('toggleTodo', id);
      },
      removeTodo(id: number) {
        this.$emit('removeTodo', id);
      },
    },
    emits: {
      toggleTodo: (id: number) => Number.isInteger(id),
      removeTodo: (id: number) => Number.isInteger(id),
    },
  });
  </script>