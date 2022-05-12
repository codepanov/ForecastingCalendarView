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
body {
  background: #21252B;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
