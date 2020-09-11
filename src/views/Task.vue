<template>
  <div class="task-view">
    <div class="flex flex-col flex-grow items-start justify-between px-4">
      <input
      type="text"
      class="p-2 mr-2 block text-xl font-bold w-full"
      :value="task.name"
      @change="updateTask($event,'name')"
      @keyup.enter="updateTask($event,'name')"
      />
      <textarea
      class="relative w-full bg-transparent px-2 border mt-2 h-64 border-none leading-normal"
      :value="task.description"
      @change="updateTask($event,'description')"
      @keyup.enter="updateTask($event,'description')"
      />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'task',
  computed: {
    ...mapGetters(['getTask']),
    task () {
      return this.getTask(this.$route.params.id)
    }
  },
  methods: {
    updateTask (e, key) {
      this.$store.commit('UPDATE_TASK', {
        task: this.task,
        key,
        value: e.target.value
      })
    }
  }
}
</script>

<style>
.task-view {
  @apply relative flex flex-row bg-white pin mx-4 m-32 mx-auto py-4 text-left rounded shadow;
  max-width: 700px;
}
</style>
