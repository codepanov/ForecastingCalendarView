<template>
  <div id="app">
    <CalendarView />
  </div>
</template>

<script>
import CalendarView from "./components/CalendarView";

export default {
  name: "App",
  components: {
    CalendarView,
  },
};
</script>

<style>
/* set the inactive (disabled) arrow color */
:root {
  --arrow-base-color: #555;
  --arrow-stop-color: red;
}
body {
  background: #21252B;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
