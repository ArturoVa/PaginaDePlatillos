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
  <div class="body">
    <div class="container-login" v-if="screen === 'login'">
      <h1>Iniciar Sesion</h1>
      <form action="" id="form">
        <div class="holder">
          <label for="">Usuario</label><input type="text" v-model="user" placeholder="Ingrese su usuario" />
        </div>
        <div class="holder">
          <label for="">Contraseña</label
          ><input type="password" v-model="password" placeholder="Ingrese su contraseña" />
        </div>
        <button id="login" type="button" @click="login">Login</button>
      </form>
    </div>
    <div class="container-post" v-else-if="screen === 'dish'">
      <div id="box">
        <h1>Platillos</h1>
        <button @click="screen = 'createDish'">Agregar Platillo</button>
        <div v-for="dish of dishes">
          <Dish :name="dish.name" :description="dish.description" :price="dish.price" :time="dish.time" />
        </div>
      </div>
    </div>

    <CreateDish v-else-if="screen === 'createDish'" @createDish="addDish" />
  </div>
</template>

<style>
.body {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  gap: 30px;
}
#login {
  width: fit-content;
  border-radius: 10px;
  border: none;
  font-size: 1.4em;
  background: #bdd358;
  align-self: center;
  padding: 10px 30px;
  transition: 1.2s;
}
#box {
  background: #ff6969;
}
#login:hover {
  background: #e5e059;
}
.holder {
  display: flex;
  width: 100%;
  justify-content: space-between;
}
#form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 40%;
  height: 40%;
}
.container-login {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #fff5e0;
  border-radius: 15px;
  height: 30%;
  width: 35%;
  flex-direction: column;
}
</style>
