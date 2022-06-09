<template>
  <div class="home">
    <ul id="Fächer">
      <li v-for="(noten, fach) in Fächer" :key="fach">
        {{ fach }}
        <ul>
          <li v-for="(note, index) in noten.noten" :key="index">
            <span>
              {{ parseFloat(note).toFixed(2) }}
              <button @click="deleteNote(fach, index)">❌</button>
            </span>
          </li>
          <li>
            <input type="number" @keyup.enter="addNote($event, fach)" />
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script setup>
// @ is an alias to /src
import { ref } from "@vue/reactivity";

const Fächer = ref({
  GES: { noten: [4, 5.5] },
  M151: { noten: [2, 5, 4] },
  M152: { noten: [6, 6] },
  M153: { noten: [6, 6] },
  M306: { noten: [6, 6] },
  NWS: { noten: [6, 6] },
  SPK: { noten: [] },
  SPO: { noten: [] },
  WUR: { noten: [] },
});
function deleteNote(fach, note) {
  console.log(Fächer.value[fach], fach, note);
  Fächer.value[fach].splice(note, 1);
}
function addNote(e, fach) {
  let newNote = Math.min(6, Math.max(1, parseInt(e.target.value)));
  Fächer.value[fach].push(newNote);
}
</script>
<style>
.home {
  display: grid;
  min-height: 100vh;
  min-width: 100vw;
  margin: 0;
  justify-content: center;
}
ul#Fächer {
  width: 50%;
}
</style>