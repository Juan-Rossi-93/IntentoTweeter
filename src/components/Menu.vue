<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container">
      <span class="navbar-brand">
        Intento de Twitter
      </span>
      <button
        class="btn pl-4 pr-4"
        :class="{ 'btn-primary': !showForm, 'btn-danger': showForm }"
        @click="openCloseForm"
      >
        {{ showForm ? "Cerrar Tweet" : "Nuevo Tweet" }}
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    showForm: Boolean,
    openCloseForm: Function,
  },
};
</script>

<style></style>
