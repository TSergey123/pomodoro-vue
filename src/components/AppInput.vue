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
              <v-btn
                @click="removeNote(index)"
                color="red-accent-3"
                rounded="lg"
                variant="tonal"
                >Удалить</v-btn
              >
            </div>
          </v-list-item>
          <div v-if="notes.length === 0"><h1>Заметок нет</h1></div>
        </v-list>
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
      // this.notes.pusj(this.inputValue)
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
