<script setup>
import { ref } from 'vue'

const nombre = ref('')
const descripcion = ref('')
const precio = ref('')
const tiempo = ref('')
const image = ref('')

const emit = defineEmits(['createDish'])

function publish() {
  emit('createDish', {
    name: nombre,
    description: descripcion,
    price: precio,
    time: tiempo,
    img: image,
  })
}
</script>

<template>
  <div class="form">
    <h1 align="center">Añadir Platillo</h1>
    <div class="input">
      <label for="">Nombre del platillo:</label>
      <input type="text" v-model="nombre" />
    </div>
    <div class="input">
      <label for="">Tiempo estimado de preparación:</label>
      <input type="text" v-model="tiempo" />
      <label for="">Precio:</label>
      <input type="number" v-model="precio" />
      <label for="">Imagen:</label>
      <input type="text" v-model="image" />
    </div>
    <div class="input">
      <label> Descripcion:</label>
      <textarea name="" id="" cols="30" rows="10" v-model="descripcion"></textarea>
      <button @click="publish" id="publish">Publicar platillo</button>
    </div>
  </div>
</template>

<style>
.input {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
}
.form {
  background: #f0b86e;
  border-radius: 10px;
  padding: 7em;
}
.form input,
.form textarea {
  outline: none;
  border: none 1px;
}
.form #publish {
  border: none;
  border-radius: 10px;
  font-size: 1.3em;
  transition: 0.5s;
  background-color: #ed7b7b;
}
.form #publish:hover {
  background-color: #bb2525;
}
</style>
