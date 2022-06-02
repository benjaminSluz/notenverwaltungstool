<template>
  <div class="home">
    <NotenListe></NotenListe>
  </div>
</template>

<script>
// @ is an alias to /src
import NotenListe from "@/components/NotenListe.vue";

export default {
  name: "HomeView",
  components: {
    NotenListe,
  },
};
</script>
