<template>
    <section class="flex flex-col gap-6">
      <form
        id="form"
        v-if="isFormVisible"
        class="flex flex-col gap-4 p-6 items-stretch border border-gray-300 rounded-3xl w-full"
        @submit.prevent="addTodo">
        <button type="button" class="self-end" @click="closeForm">
          <i class="cursor-pointer">
            <svg
              class="h-4 w-4 text-gray-700"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round">
              <line x1="18" y1="6" x2="6" y2="18" />
              <line x1="6" y1="6" x2="18" y2="18" />
            </svg>
          </i>
        </button>
        <div>
          <input
            type="text"
            class="w-full p-2 border border-red-700 rounded-3xl"
            v-model="todoText" />
        </div>
        <button class="bg-red-700 rounded-3xl p-2 border text-white">
          Add task
        </button>
      </form>
      <button
        v-else
        class="border border-gray-300 rounded-3xl w-full"
        @click="showForm">
        <i class="p-4 flex justify-center w-full">
          <svg
            class="h-6 w-6 text-red-600"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor">
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 4v16m8-8H4" />
          </svg>
        </i>
      </button>
    </section>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  //@ts-ignore
  import {type Todo } from '../types/Todo';
  
  interface State {
    isFormVisible: boolean;
    todoText: string;
  }
  
  export default defineComponent({
    data(): State {
      return {
        isFormVisible: false,
        todoText: '',
      };
    },
    methods: {
      showForm() {
        this.isFormVisible = true;
      },
      closeForm() {
        this.isFormVisible = false;
      },
      addTodo() {
        this.$emit('addTodo', {
          id: Date.now(),
          text: this.capitalizeFirstLetter,
          completed: false,
        });
        this.todoText = '';
      },
    },
    computed: {
      capitalizeFirstLetter(): string {
        return this.todoText.charAt(0).toUpperCase() + this.todoText.slice(1)
      }
    },
    emits: {
      addTodo: (todo: Todo) => todo,
    },
  });
  </script>