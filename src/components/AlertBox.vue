<script setup>
import { onMounted, onUnmounted } from 'vue'
import { Icon } from '@iconify/vue';

const props = defineProps({
  mensaje: String,
  tipo: {
    validator(value) {
      // Valor de la prop debe coincidir con uno de los valores del array
      return ['success', 'error', 'info'].includes(value)
    }
  }
})

const alertIcon = () => {
  switch (props.tipo) {
    case 'success':
      return 'lucide:square-check'
    case 'error':
      return 'lucide:message-circle-warning'
    case 'info':
      return 'lucide:info'
  }
}

onMounted(() => {
  console.log('Se monta componente AlertBox')
})

onUnmounted(() => {
  console.log('Se desmonta componente AlertBox')
})
</script>

<template>
  <div class="alert" :class="`alert--${tipo}`">
    <div class="alert__header">
      <Icon :icon="alertIcon()" class="alert__icon" />
      <h2>{{ mensaje }}</h2>
    </div>
  </div>
</template>

<style scoped>
.alert {
  padding: 0.4rem 1rem;
  margin: 10px;
  border-radius: 10px;
}

.alert__header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
}

.alert__icon {
  width: 30px;
  height: 30px;
}

.alert--success {
  background-color: rgba(172, 255, 47, 0.123);
  color: green;
}

.alert--error {
  background-color: rgba(255, 0, 0, 0.114);
  color: red;
}

.alert--info {
  background-color: lightblue;
  color: rgb(24, 131, 198);
}
</style>