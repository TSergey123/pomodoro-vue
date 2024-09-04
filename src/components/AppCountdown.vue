<template>
  <v-container>
    <v-card class="mx-auto" max-width="400">
      <v-card-title>Обратный отсчёт</v-card-title>
      <v-card-text>
        <v-text-field
          v-model="inputMinutes"
          label="Минуты"
          type="number"
          min="1"
          max="60"
          @blur="updateTime"
          :disabled="isRunning"
        ></v-text-field>
        <div class="text-h4 text-center">{{ formattedTime }}</div>
        <v-progress-linear
          model-value="25"
          :value="inputMinutes"
          height="10"
          color="blue"
          class="mt-4"
        ></v-progress-linear>
      </v-card-text>
      <v-card-actions>
        <v-btn @click="startTimer" :disabled="isRunning || time.value === 0">Старт</v-btn>
        <v-btn @click="pauseTimer" :disabled="!isRunning">Пауза</v-btn>
        <v-btn @click="resetTimer">Сброс</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref, computed } from 'vue'

const inputMinutes = ref(25)
const time = ref(0)
const isRunning = ref(false)
let timerInterval = null
const initialTime = ref(0)

const formattedTime = computed(() => {
  const minutes = Math.floor(time.value / 60)
  const seconds = time.value % 60
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`
})

const progressLine = computed(() => {
  // return (time.value / initialTime.value) * 100
  return inputMinutes;
})

const updateTime = () => {
  initialTime.value = inputMinutes.value * 60
  time.value = initialTime.value
}

const startTimer = () => {
  if (!isRunning.value && time.value > 0) {
    isRunning.value = true
    timerInterval = setInterval(() => {
      if (time.value > 0) {
        time.value -= 1
      } else {
        clearInterval(timerInterval)
        isRunning.value = false
      }
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
  updateTime()
}
</script>

<style scoped>
.text-center {
  text-align: center;
}
</style>
