<template>
  <v-container>
    <v-card class="mx-auto" max-width="400">
      <v-card-title>Таймер</v-card-title>
      <v-card-text>
        <div class="text-h4 text-center">{{ formattedTime }}</div>
      </v-card-text>
      <v-card-actions>
        <v-btn @click="startTimer" :disabled="isRunning">Старт</v-btn>
        <v-btn @click="pauseTimer" :disabled="!isRunning">Пауза</v-btn>
        <v-btn @click="resetTimer">Сброс</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref, computed } from 'vue'

const time = ref(0)
const isRunning = ref(false)
let timerInterval = null

const formattedTime = computed(() => {
  const minutes = Math.floor(time.value / 60)
  const seconds = time.value % 60
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`
})

const startTimer = () => {
  if (!isRunning.value) {
    isRunning.value = true
    timerInterval = setInterval(() => {
      time.value += 1
    }, 1000)
  }
}

const pauseTimer = () => {
  if (isRunning.value) {
    isRunning.value = false
    clearInterval(timerInterval)
  }
}

const resetTimer = () => {
  isRunning.value = false
  clearInterval(timerInterval)
  time.value = 0
}
</script>

<style scoped>
.text-center {
  text-align: center;
}
</style>
