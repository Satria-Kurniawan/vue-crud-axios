<template>
  <div class="card mb-2" :class="[task.reminder ? 'statusMark' : 'card']">
    <div class="card-header">
      <h4>{{ task.title }}</h4>
    </div>
    <div class="card-body row">
      <div class="col-lg-9">
        <h6>{{ task.description }}</h6>
        <h5>{{ task.deadline }}</h5>
      </div>
      <div class="col-lg-3 text-end">
        <Button
          @click="$emit('handleEdit', task)"
          :text="'edit'"
          :btnColor="'blue'"
          :txtColor="'white'"
          class="cus-btn mb-1"
        />
        <Button
          @click="$emit('handleDelete', task.id)"
          :text="'delete'"
          :btnColor="'red'"
          :txtColor="'white'"
          class="cus-btn ms-1 mb-1"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Button from "../../Button.vue"

export default {
  name: "Task",
  props: {
    task: Object,
  },
  components: {
    Button,
  },
}
</script>

<style>
.statusMark {
  border-left: 4px solid red;
}
</style>
