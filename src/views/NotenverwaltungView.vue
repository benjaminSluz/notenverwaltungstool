<template>
  <div class="home">
    <ul id="Fächer">
      <li v-for="(noten, fach) in Fächer" :key="fach">
        <span class="Fach"> {{ fach }}</span>
        <ul>
          <li v-for="(note, index) in noten.noten" :key="index">
            <span>
              {{ parseFloat(note).toFixed(2) }}
              <button @click="deleteNote(fach, index)">❌</button>
            </span>
          </li>
          <div>
            <div>Abschluss Note:{{ avgNote(noten.noten) }}</div>
            <label>
              Neue Note einfügen:
              <input type="number" @keyup.enter="addNote($event, fach)" />
            </label>
          </div>
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
  SPK: { noten: [4.24, 5.7] },
  SPO: { noten: [4.8, 3.21] },
  WUR: { noten: [6, 2.4] },
});
function deleteNote(fach, note) {
  console.log(Fächer.value[fach].noten, fach, note);
  Fächer.value[fach].noten.splice(note, 1);
}
function addNote(e, fach) {
  let newNote = Math.min(6, Math.max(1, parseInt(e.target.value)));
  Fächer.value[fach].noten.push(newNote);
}
function avgNote(noten) {
  let notenArray = [...noten];
  if (notenArray.length == 0) return 0;
  let avg = 0;
  let result;
  notenArray.forEach((e) => {
    avg += e;
  });
  avg /= notenArray.length;

  result = Math.floor(avg) + Math.round((avg % 1) * 2) / 2;
  return parseFloat(result).toFixed(2);
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
ul {
  padding-inline-start: 20px;
  border: 1px black solid;
}
.Fach {
  font-weight: bolder;
}
#Fächer {
  border: black 1px solid;
  height: fit-content;
}
</style>