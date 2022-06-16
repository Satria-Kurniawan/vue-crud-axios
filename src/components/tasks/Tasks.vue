<template>
  <div class="row">
    <div class="col-lg-12">
      <div :key="task.id" v-for="task in tasks">
        <Task
          :task="task"
          @handleEdit="$emit('handleEdit', task)"
          @handleDelete="$emit('handleDelete', task.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Task from "./task/Task.vue"

export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
}
</script>

<style></style>
