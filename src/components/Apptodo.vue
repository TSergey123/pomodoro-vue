<template>
  <v-container>
    <v-card class="d-flex flex-column align-md-center">
      <h1
        :style="{
          color: inputValue.length < 10 ? '' : 'teal',
        }"
      >
        {{ title }}
      </h1>
      <v-col cols="12">
        <v-text-field
          :rules="rules"
          hide-details="auto"
          :label="placeholder"
          v-model="inputValue"
          @keypress.enter="addNewNote"
        ></v-text-field>
        <p>{{ inputValue }}</p>
        <v-btn
          @click="addNewNote"
          class="mt-3"
          color="teal-accent-3"
          rounded="lg"
          variant="tonal"
        >
          Добавить
        </v-btn>
        <AppList :notes="notes" @start-timer="$emit('start-timer')"/>
        <div>
          <p>Всего Заметок: {{ notes.length }}</p>
          <p>Дабл Заметок: {{ doubleCount() }}</p>
        </div>
      </v-col>
    </v-card>
  </v-container>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    title: {
      type: String,
      default: "Список",
    },
    placeholder: {
      type: String,
      default: "Введите текст",
    },
    initialNotes: {
      type: Array,
      default: () => ["Заметка_1", "Заметка_2"],
    },
    inputValue: {
      type: String,
      default: "",
    },
  },
  setup(props) {
    const inputValue = ref("");
    const notes = ref([...props.initialNotes]);

    const addNewNote = () => {
      // this.notes.push(this.inputValue)
      if (inputValue.value.trim()) {
        notes.value.push(inputValue.value);
        inputValue.value = ""; // Очистить поле ввода после добавления
      }
    };

    const doubleCount = () => {
      return notes.value.length * 2;
    };

    const removeNote = (index) => {
      notes.value.splice(index, 1);
    };

    return {
      title: props.title,
      placeholder: props.placeholder,
      inputValue,
      notes,
      addNewNote,
      removeNote,
      doubleCount,
    };
  },
  watch: {
    inputValue(value) {
      if (value.length > 10) {
        this.inputValue = "";
      }
    },
  },
};
</script>
