<template>
  <div id="app">
    <ScrollBar></ScrollBar>
  </div>
</template>

<script>
import ScrollBar from "./components/ScrollBar/Index";

export default {
  name: "App",
  components: {
    ScrollBar
  }
};
</script>

<style>
#app {
  width: 100%;
  height: 100%;
}
</style>
