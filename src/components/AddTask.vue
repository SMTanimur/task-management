<template>
  <form
    @submit.prevent="handleSubmit"
    class="space-y-7 flex-grow rounded-2xl shadow-2xl p-5 font-bold"
  >
    <div class="form-control w-full max-w-xs">
      <label class="label">
        <span class="label-text">Title</span>
      </label>
      <input
        type="text"
        v-model.trim="title"
        placeholder="e.g. Create New App"
        class="input border-2 px-2 py-3 focus:ring-2 w-full max-w-xs"
        maxlength="50"
        required
      />
    </div>

    <div class="flex flex-col space-y-2">
      <label class="label">
        <span class="label-text">Details</span>
      </label>
      <textarea
        class="border h-24 resize-none"
        v-model.trim="details"
        placeholder="e.g. Create a new app using Vuejs and Tailwindcss"
        maxlength="250"
        required
      ></textarea>
    </div>
    <div class="text-center md:text-start">
      <button class="bg-rose-500 px-4 py-2 text-white rounded-lg">Add Task</button>
    </div>
  </form>
</template>

<script>
import { uuid } from 'vue-uuid'
export default {
  name: 'AddTask',
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit() {
      let newTask = {
        id: uuid.v1(),
        title: this.title,
        details: this.details,
        completed: false
      }
      this.$emit('newTask', newTask)
      this.title = ''
      this.details = ''
    }
  }
}
</script>
