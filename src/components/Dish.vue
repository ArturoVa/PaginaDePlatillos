<script setup>
defineProps({
  name: String,
  description: String,
  price: String,
  time: String, //tiempo de preparacion
})
</script>
<template>
  <div class="container">
    <h3>{{ name }}</h3>
    <p>{{ description }}</p>
    <br />
    <b>${{ price }}</b>
    <br />
    <span>tiempo de preparacion: {{ time }}</span>
  </div>
</template>

<style>
.container {
  width: 50vw;
  height: 20vh;
  background: grey;
}
</style>
