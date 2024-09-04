<template>
  <v-row fluid>
    <v-checkbox
      v-for="(checked, index) in checkboxes"
      :key="index"
      v-model="localCheckboxes[index]"
      :label="`Checkbox ${index + 1}`"
    ></v-checkbox>
    <v-btn
      class="mt-3"
      color="pink-accent-3"
      rounded="lg"
      variant="tonal"
      @click="handleLogAndStartTimer"
    >
      Консоль лог
    </v-btn>
  </v-row>
</template>

<script>
export default {
  props: {
    checkboxes: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      localCheckboxes: [...this.checkboxes],
    };
  },
  watch: {
    localCheckboxes: {
      handler(newVal) {
        this.$emit('update:checkboxes', newVal);
      },
      deep: true,
    },
  },
  methods: {
    showLog() {
      console.log(this.localCheckboxes);
    },

    //Ну тут я уже просто поплыл
    handleLogAndStartTimer() {
      this.showLog();
      this.$emit('start-timer');
    },
  },
};
</script>
