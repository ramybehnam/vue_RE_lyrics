<template>
  <div class="home">
    <RELyrics />
  </div>
</template>

<script>
// @ is an alias to /src
import RELyrics from "@/components/HomePage.vue";

export default {
  name: "Home",
  components: {
    RELyrics
  }
};
</script>
