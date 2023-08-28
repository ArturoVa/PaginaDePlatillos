<script setup>
import { ref } from 'vue'
import Dish from './Dish.vue'
import CreateDish from './CreateDish.vue'

const screen = ref('login')

class Platillo {
  constructor(name, description, price, time, image) {
    this.name = name
    this.description = description
    this.price = price
    this.time = time
    this.image = image
  }
}

const initialDishes = [new Platillo('Nombre', 'descripcion', 'precio', 'tiempo', 'imagenn')]
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
        <div id="title">
          <h1>Platillos</h1>
          <button @click="screen = 'createDish'" id="buttonAdd">Agregar Platillo</button>
        </div>
        <hr color="black" />
        <div id="displayList">
          <div v-for="dish of dishes">
            <Dish
              :name="dish.name"
              :description="dish.description"
              :price="dish.price"
              :time="dish.time"
              :img="dish.image"
            />
          </div>
        </div>
      </div>
    </div>

    <CreateDish v-else-if="screen === 'createDish'" @createDish="addDish" />
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  box-sizing: border-box;
}
.body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 100vw;
  width: 100vw;

  height: 100vh;
  gap: 30px;
  box-sizing: border-box;
}
#login {
  width: fit-content;
  border-radius: 10px;
  border: none;
  font-size: 1.4em;
  background: #bdd358;
  align-self: center;
  padding: 10px 30px;
  transition: 0.5s;
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
.container-post {
  background: #e19898;
  width: 80%;
  min-height: 80%;
  padding: 30px;
  border-radius: 10px;
  box-sizing: border-box;
}
.container-login {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #e19898;
  border-radius: 15px;
  height: 40%;
  width: 35%;
  flex-direction: column;
}
#title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: transparent;
}
#buttonAdd {
  border-radius: 10px;
  border: none;
  font-size: 1.3em;
  color: none;
  background-color: #ebe76c;
  transition: 0.5s;
}
#buttonAdd:hover {
  transform: scale(1.2);
}
#displayList {
  max-height: 65vh;
  overflow: auto;
  height: 100%;
}
</style>
