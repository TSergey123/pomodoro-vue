<template>
  <v-list class="border-b-md border-success">
    <v-list-item :key="index" v-for="(note, index) in notes">
      <div class="d-flex justify-space-between">
        <h3
          :style="{
            color: note.length < 10 ? '' : 'teal',
          }"
          :class="{
            primary: note.length > 10,
          }"
        >
          [{{ index }}]{{ note }}
        </h3>
        <AppEstimated :checkboxes="checkboxes" @start-timer="$emit('start-timer')" />
        <v-btn
          @click="removeNote(index)"
          color="red-accent-3"
          rounded="lg"
          variant="tonal"
        >Удалить</v-btn>
      </div>
    </v-list-item>
    <div v-if="notes.length === 0"><h1>Заметок нет</h1></div>
  </v-list>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      checkboxes: [false, false, false, false],
    };
  },
};
</script>
