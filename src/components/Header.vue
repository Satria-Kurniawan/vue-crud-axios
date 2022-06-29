<template>
  <nav class="navbar navbar-expand-lg bg-white">
    <div class="container-fluid">
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto me-auto">
          <!-- <li class="nav-item">
            <router-link
              to="/"
              class="nav-link"
              :class="{ active: $route.name === 'home' }"
              >Home</router-link
            >
          </li> -->
          <li class="nav-item">
            <router-link
              to="/"
              class="nav-link"
              :class="{ active: $route.name === 'tasks' }"
              >Tasks</router-link
            >
          </li>
          <li class="nav-item">
            <router-link
              to="/about"
              class="nav-link"
              :class="{ active: $route.name === 'about' }"
              >About</router-link
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {}
</script>

<style>
.active {
  border-bottom: 3px solid rgb(195, 0, 255);
}
</style>
