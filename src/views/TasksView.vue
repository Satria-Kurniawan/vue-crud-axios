<template>
  <div class="container">
    <h1 class="text-center">This is a tasks view</h1>
    <div class="d-flex">
      <Button
        @click="toggleForm"
        :text="showForm ? 'close' : 'create'"
        :btnColor="showForm ? 'red' : 'green'"
        :txtColor="'white'"
        class="cus-btn mb-3 ms-auto"
      />
    </div>
    <div class="position-absolute top-50 start-50 translate-middle">
      <div
        :class="[loading ? 'spinner-border text-primary ms-4' : '']"
        style="width: 3rem; height: 3rem"
      />
      <br /><br />
      <h4>{{ loading ? "Loading..." : "" }}</h4>
    </div>
    <div class="row">
      <div :class="showForm ? 'col-lg-8' : 'col-lg-12'">
        <Tasks
          :tasks="tasks"
          @handleEdit="editTask"
          @handleDelete="deleteTask"
        />
      </div>
      <div :class="showForm ? 'col-lg-4' : ''">
        <Form
          v-show="showForm"
          @formData="storeTask"
          @formDataEdited="updateTask"
          :form="form"
          :showBtnCreate="showBtnCreate"
          :showBtnUpdate="showBtnUpdate"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import Tasks from "../components/tasks/Tasks.vue"
import Button from "../components/Button.vue"
import Form from "../components/Form.vue"

export default {
  name: "NoteView",
  components: {
    Tasks,
    Button,
    Form,
  },
  data() {
    return {
      tasks: [],
      loading: false,
      showForm: false,
      showBtnCreate: false,
      showBtnUpdate: false,
      form: {
        id: "",
        title: "",
        description: "",
        deadline: "",
        reminder: false,
      },
    }
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm
      this.showBtnCreate = true
      this.showBtnUpdate = false

      // untuk ngeclear form bekas edit
      if (!this.showForm) {
        this.form.title = ""
        this.form.description = ""
        this.form.deadline = ""
        this.form.reminder = false
      }
    },
    getTasks() {
      this.loading = true
      axios
        .get("https://62a7032797b6156bff84ef49.mockapi.io/api/tasks")
        .then((res) => (this.tasks = res.data))
        .catch((err) => console.error(err))
        .finally(() => (this.loading = false))
    },
    storeTask(task) {
      axios
        .post("https://62a7032797b6156bff84ef49.mockapi.io/api/tasks", task)
        .then((res) => (this.tasks = [...this.tasks, res.data]))
        .catch((err) => console.error(err))

      this.showForm = !this.showForm
    },
    editTask(task) {
      // kalau form udah kebuka, langsung masukin isi form yang mau di edit
      // kalau form masih ketutup, buka dulu, baru masukin isi form yang mau di edit
      if (this.showForm) {
        this.form = { ...this.form, ...task }
        this.showBtnCreate = false
        this.showBtnUpdate = true
      } else {
        this.showForm = !this.showForm
        this.form = { ...this.form, ...task }
        this.showBtnCreate = false
        this.showBtnUpdate = true
      }
    },
    updateTask(task) {
      axios
        .put(
          "https://62a7032797b6156bff84ef49.mockapi.io/api/tasks/" +
            this.form.id,
          task
        )
        .then(
          (res) =>
            (this.tasks = this.tasks.map((item) =>
              item.id === this.form.id ? { ...item, ...res.data } : item
            ))
        )
        .catch((err) => console.error(err))

      this.showForm = !this.showForm
    },
    deleteTask(id) {
      axios
        .delete("https://62a7032797b6156bff84ef49.mockapi.io/api/tasks/" + id)
        .then(
          (res) =>
            (this.tasks = this.tasks.filter((task) => task.id !== res.data.id))
        )
    },
  },
  created() {
    this.getTasks()
  },
}
</script>

<style>
.cus-btn {
  width: 90px;
  text-transform: uppercase;
}
.cus-btn:hover {
  transform: scale(1.1);
  transition: 0.2s ease-in;
}
</style>
