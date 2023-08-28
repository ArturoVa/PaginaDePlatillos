<script setup>
import { ref } from 'vue'
import Dish from './Dish.vue'
import CreateDish from './CreateDish.vue'

const screen = ref('login')

class Platillo {
  constructor(name, description, price, time) {
    this.name = name
    this.description = description
    this.price = price
    this.time = time
  }
}

const initialDishes = [new Platillo('Nombre', 'descripcion', 'precio', 'tiempo')]
const dishes = ref(JSON.parse(window.localStorage.getItem('dish')) ?? initialDishes)
const user = ref('')
const password = ref('')

const USER = 'arturo'
const PASSWORD = '123'

function login() {
  if (user.value !== USER) {
    alert('Usuario incorrecto')
  } else if (password.value !== PASSWORD) {
    alert('Contraseña incorrecta')
  } else {
    screen.value = 'dish'
  }
}

function addDish(newDish) {
  dishes.value.push(newDish)
  screen.value = 'dish'
  window.localStorage.setItem('dishes', JSON.stringify(dishes.value))
}
</script>

<template>
  <div class="container-login" v-if="screen === 'login'">
    <form action="" id="form">
      <div class="holder"><label for="">User</label><input type="text" v-model="user" /></div>
      <div class="holder"><label for="">Password</label><input type="password" v-model="password" /></div>
      <button id="login" type="button" @click="login">Login</button>
    </form>
  </div>
  <div class="container-post" v-else-if="screen === 'dish'">
    <h1>Platillos</h1>
    <button @click="screen = 'createDish'">Agregar Platillo</button>
    <div v-for="dish of dishes">
      <Dish :name="dish.name" :description="dish.description" :price="dish.price" :time="dish.time" />
    </div>
  </div>
  <CreateDish v-else-if="screen === 'createDish'" @createDish="addDish" />
</template>
