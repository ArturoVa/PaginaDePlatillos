<script setup>
defineProps({
  name: String,
  description: String,
  price: String,
  time: String, //tiempo de preparacion
  img: String,
})
</script>
<template>
  <div class="container">
    <h3 class="title">{{ name }}</h3>
    <div class="text">
      <p>{{ description }}</p>
      <b>${{ price }}</b>
      <br />
      <span>tiempo de preparacion: {{ time }}</span>
    </div>
    <img :src="img" alt="aqui va una imagen" class="image" />
  </div>
</template>

<style>
.container {
  display: flex;
  width: 100%;
  min-height: 40%;
  padding: 10px;
  box-sizing: border-box;
  background: #141e46;
  color: beige;
  justify-content: space-around;
  align-items: center;
  border-radius: 5px;
}
.container .title {
  min-width: 20%;
  max-width: 20%;
}
.container .text {
  min-width: 50%;
  max-width: 50%;
}
.container .image {
  min-width: 30%;
  max-width: 30%;
}
</style>
