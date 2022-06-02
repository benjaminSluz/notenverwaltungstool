<template>
  <div class="home">
    <ul>
      <li v-for="(note, fach) in Fächer" :key="fach">
        {{ fach }}
      </li>
    </ul>
  </div>
</template>

<script setup>
// @ is an alias to /src
import { ref } from "@vue/reactivity";

const Fächer = ref({
  M151: [2],
});
</script>
