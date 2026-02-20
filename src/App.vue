<script setup>
import { ref, computed } from 'vue'
import AlertBox from './components/AlertBox.vue';

const alerts = [
  {
    mensaje: 'Operación exitosa',
    tipo: 'success'
  },
  {
    mensaje: 'Operación fallida',
    tipo: 'error'
  },
  {
    mensaje: 'Información importante',
    tipo: 'info'
  }
]

const amount = ref(1)

const alertsByAmount = computed(() => {
  return alerts.slice(0, amount.value)
})

</script>

<template>
  <main class="main">
    <h1>AlertBox</h1>
    <TransitionGroup name="alert">
      <AlertBox v-for="alert in alertsByAmount" :key="alert.tipo" :mensaje="alert.mensaje" :tipo="alert.tipo" />
    </TransitionGroup>

    <section class="buttons">
      <button @click="amount++" :disabled="amount >= alerts.length">Agregar alerta</button>
      <button @click="amount--" :disabled="amount < 1">Quitar alerta</button>
    </section>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

.main {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: center;
  height: calc(100vh - 1rem);
  width: 800px;
  margin: 0 auto;
}

h1 {
  text-align: center;
  margin-bottom: 2rem;
}

.buttons {
  display: flex;
  justify-content: center;
}

button {
  margin: 0.6rem;
  padding: 0.8rem;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  background-color: rgb(85, 119, 255);
  color: white;
}

button:hover {
  background-color: rgb(34, 78, 253);
}

button:disabled {
  background-color: gray;
  cursor: not-allowed;
}

/* Transiciones */
.alert-enter-active,
.alert-leave-active {
  transition: all 0.5s ease;
}

.alert-enter-from,
.alert-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
