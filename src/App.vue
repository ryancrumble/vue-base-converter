<template>
  <div id="app" class="has-background-warning-light">
    <div class="container">
      <base-converter />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BaseConverter from "./components/BaseConverter.vue";

@Component({
  components: {
    BaseConverter
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100vh;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70%;
  height: 100%;
}
</style>
