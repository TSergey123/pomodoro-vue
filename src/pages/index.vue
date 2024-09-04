<template>
  <AppTimer />
  <AppCountdown ref="appCountdown" />
  <Apptodo @start-timer="startTimer" />
</template>

<script setup>
import { ref } from 'vue';

const appCountdownRef = ref(null);

const startTimer = () => {
  if (appCountdownRef.value) {
    appCountdownRef.value.startTimer();
  }
};
</script>
