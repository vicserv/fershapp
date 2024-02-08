<script setup>
import { ref } from 'vue';
import Swal from 'sweetalert2';

const message = ref(' Haz clic en el boton para ver cuanto te quiero');
const showHeart = ref(false);
const hearts = ref(0);

const addHeart = () => {
  hearts.value++;
};

const lovesMessagesInitial = [
  'Eres mi todo Princesita ❤️',
  'Me gustas mucho Fer ❤️',
  'Fer, todo es mas bonito contigo ❤️',
  'Tu sonrisa es mi mayor felicidad ❤️',
  'Tu voz es mi cancion favorita ❤️',
  'Eres hermosa ❤️',
  'Me haces muy feliz ❤️',
  'Soy un adicto a ti ❤️',
  'Cada minuto pienso en ti ❤️',
  'Te amo Fer ❤️',
];

const lovesMessages = ref([...lovesMessagesInitial]);

const showLove = () => {
  const randomIndex = Math.floor(Math.random() * lovesMessages.value.length);
  message.value = lovesMessages.value[randomIndex];
  showHeart.value = true;
  addHeart();
  setTimeout(() => {
    showHeart.value = false;
  }, 2000);
  // delete index from array
  lovesMessages.value.splice(randomIndex, 1);

  if (hearts.value === 10) {
    Swal.fire({
      title: '¡Felicidades!',
      text: 'Te ganaste mi corazon, te quiero Fer ❤️❤️❤️❤️❤️❤️❤️❤️❤️❤️',
      icon: 'success',
      confirmButtonText: '¡Te Quiero!',
    });

    hearts.value = 0;
    lovesMessages.value = [...lovesMessagesInitial];
    message.value = 'Haz clic en el boton para ver cuanto te quiero';
  }
};
</script>

<template>
  <!-- center the icon  -->
  <div
    style="
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 25vh;
      margin: 0;
      padding: 0;
    "
  >
    <icon
      @click="addHeart"
      :style="{
        fontSize: `${hearts < 9 ? hearts * 0.4 : 5}em `,
        color: hearts < 9 ? 'red' : 'gold',
        position: 'fixed',
        top: '100px',

        margin: 0,
        padding: 0,
      }"
    >
      ❤️</icon
    >
  </div>

  <div id="app" class="container">
    <h1>¡La App de Fer!</h1>
    <h2 :class="{ heart: showHeart }">{{ message }}</h2>
    <button @click="showLove" :disabled="showHeart">
      {{
        // Mostrar amor , aun hay mas amor
        showHeart ? 'Da click nuevamente' : 'Mostrar Amor'
      }}
    </button>

    <p>Corazones: {{ hearts }}</p>
  </div>
</template>

<style scoped>
button {
  padding: 1em 2em;
  font-size: 1.5em;
  cursor: pointer;
  border: none;
  border-radius: 0.5em;
  background-color: #646cff;
  color: white;
  transition: background-color 300ms;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.container {
  text-align: center;
  margin-top: 50px;
}
button {
  padding: 10px 20px;
  font-size: 18px;
  margin: 10px;
}
.heart {
  color: red;
  animation: pulse 1s infinite alternate;
}
@keyframes pulse {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(1.1);
  }
}
</style>
