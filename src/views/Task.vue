<template>
  <div class="task-view">
    <div class="flex flex-col flex-grow items-start justify-between px-4">
      <input
        type="text"
        class="block p-2 mr-2 text-xl font-bold focus:outline-none w-full"
        :value="task.name"
        @change="updateTaskProperty($event, 'name')"
        @keyup.enter="updateTaskProperty($event, 'name')"
      />
      <textarea
        class="relative bg-transparent px-2 border border-none mt-2 leading-normal focus:outline-none h-64 block w-full text-grey-dark"
        :value="task.description"
        placeholder="description.."
        @change="updateTaskProperty($event, 'description')"
      />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  computed: {
    ...mapGetters(['getTask']),
    task() {
      return this.getTask(this.$route.params.id)
    }
  },
  methods: {
    updateTaskProperty(e, key) {
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
