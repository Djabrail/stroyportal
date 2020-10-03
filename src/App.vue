<template>
  <div id="app">
    <Header />
  </div>
</template>

<script>
import "normalize.css";
import Header from "@/components/Header";

export default {
  name: "App",
  components: {
    Header
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap");
body {
  font-family: "Open Sans", sans-serif;
}

.container {
  max-width: 1110px;
  margin: 0 auto;
  padding-left: 20px;
  padding-right: 20px;
}
input:focus {
  outline: none;
}
</style>
