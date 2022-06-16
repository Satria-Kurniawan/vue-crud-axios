<template>
  <div class="card">
    <div class="card-body">
      <form @submit.prevent="showBtnCreate ? handleSave() : handleUpdate()">
        <div class="col-lg-12 mb-2">
          <label for="title">Title</label>
          <input type="text" v-model="form.title" class="form-control" />
        </div>
        <div class="col-lg-12 mb-2">
          <label for="description">Description</label>
          <textarea v-model="form.description" class="form-control" />
        </div>
        <div class="col-lg-12 mb-2">
          <label for="deadline">Deadline</label>
          <input type="text" v-model="form.deadline" class="form-control" />
        </div>
        <div class="col-lg-12 mb-2">
          <label class="form-check-label" for="reminder">Reminder</label>
          <input
            class="form-check-input ms-2"
            type="checkbox"
            v-model="form.reminder"
          />
        </div>
        <div class="col-lg-3">
          <Button
            v-show="showBtnCreate"
            type="submit"
            :text="'save'"
            :btnColor="'green'"
            :txtColor="'white'"
            class="cus-btn mb-3"
          />
        </div>
        <div class="col-lg-3">
          <Button
            v-show="showBtnUpdate"
            type="submit"
            :text="'update'"
            :btnColor="'blue'"
            :txtColor="'white'"
            class="cus-btn mb-3"
          />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue"

export default {
  name: "Form",
  components: {
    Button,
  },
  props: {
    showBtnCreate: Boolean,
    showBtnUpdate: Boolean,
    form: {
      id: String,
      title: String,
      description: String,
      deadline: String,
      reminder: Boolean,
    },
  },
  methods: {
    handleSave() {
      const newTask = {
        title: this.form.title,
        description: this.form.description,
        deadline: this.form.deadline,
        reminder: this.form.reminder,
      }

      this.$emit("formData", newTask)

      this.form.title = ""
      this.form.description = ""
      this.form.deadline = ""
      this.form.reminder = false
    },
    handleUpdate() {
      const newTask = {
        title: this.form.title,
        description: this.form.description,
        deadline: this.form.deadline,
        reminder: this.form.reminder,
      }

      this.$emit("formDataEdited", newTask)

      this.form.title = ""
      this.form.description = ""
      this.form.deadline = ""
      this.form.reminder = false
    },
  },
}
</script>

<style></style>
