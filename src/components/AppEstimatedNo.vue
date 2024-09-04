<template>
  <div>
    <ul>
      <li>
        <!-- Не получается загрузить svg ;( -->
        <!-- <v-img
        class="mb-4"
        height="150"
        :src="require('@/assets/logo.png')"
      /> -->
        <div @click="toggleCheckbox('checkbox1')" style="cursor: pointer;">
          <v-img
            :src="checkbox1 ? '@/assets/logo.png' : '@/assets/logo.png'"
            alt="Checkbox 1"
            height="150"
            max-width="50"
          ></v-img>
          <span>Checkbox 1: {{ checkbox1.toString() }}</span>
        </div>
        <div @click="toggleCheckbox('checkbox2')" style="cursor: pointer;">
          <v-img
            :src="checkbox2 ? '/assets/logo.png' : '/assets/logo.png'"
            alt="Checkbox 2"
            max-width="50"
          ></v-img>
          <span>Checkbox 2: {{ checkbox2.toString() }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checkbox1: true,
      checkbox2: false,
      logopath: '@/assets/logo.png'
    };
  },
  methods: {
    toggleCheckbox(checkbox) {
      this[checkbox] = !this[checkbox];
    },
  },
};
</script>
