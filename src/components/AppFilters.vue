<template>
  <aside class="mt-10 w-full">
    <section
      class="grid grid-cols-3 border border-gray-200 rounded-3xl text-2xl">
      <button
        v-for="filter in filters"
        :key="filter"
        class="px-4 py-2 hover:text-red-600"
        :class="{
          'text-red-600 border-2 border-red-600 rounded-3xl':
            activeFilter === filter,
        }"
        @click="setFilter(filter)">
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { type PropType, defineComponent } from 'vue';
//@ts-ignore
import {type Filter } from '../types/Filter';

interface State {
  filters: Filter[];
}

export default defineComponent({
  data(): State {
    return {
      filters: ['All', 'Active', 'Done'],
    };
  },
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true,
    },
  },
  methods: {
    setFilter(filter: Filter) {
      this.$emit('setFilter', filter);
    },
  },
  emits: {
    setFilter: (filter: Filter) => filter,
  },
});
</script>