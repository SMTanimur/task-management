<template>
  <li
    class="group w-full grid grid-cols-[2.4rem_1fr_1.6rem] justify-stretch gap-6 px-8 py-4 items-center cursor-pointer border border-gray-300 rounded-3xl"
    :class="{ 'line-through': todo.completed }"
    @click="toggleTodo">
    <div>
      <i :class="todo.completed ? 'visible' : 'invisible'">
        <svg
          class="h-8 w-8 text-red-600"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          fill="none"
          stroke-linecap="round"
          stroke-linejoin="round">
          <path stroke="none" d="M0 0h24v24H0z" />
          <path d="M5 12l5 5l10 -10" />
        </svg>
      </i>
    </div>
    <span>{{ todo.text }}</span>
    <button @click.stop="removeTodo">
      <i>
        <svg
          class="h-5 w-5 opacity-0 text-gray-300 duration-300 group-hover:opacity-100 hover:opacity-100 hover:text-red-600"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round">
          <polyline points="3 6 5 6 21 6" />
          <path
            d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2" />
          <line x1="10" y1="11" x2="10" y2="17" />
          <line x1="14" y1="11" x2="14" y2="17" />
        </svg>
      </i>
    </button>
  </li>
</template>

<script lang="ts">
//@ts-ignore
import {type Todo } from '../types/Todo';
import { type PropType, defineComponent } from 'vue';

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    },
  },
  methods: {
    toggleTodo() {
      this.$emit('toggleTodo', this.todo.id);
    },
    removeTodo() {
      this.$emit('removeTodo', this.todo.id);
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
});
</script>