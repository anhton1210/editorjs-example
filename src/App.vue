<template>
  <div id="app">
    <editor-comp />
  </div>
</template>

<script>
import EditorComp from "./components/EditorComp.vue"

export default {
  components: {
    EditorComp
  },
  data() {
    return {
      value: null,
    };
  },
  methods: {
  },
};
</script>

<style lang="css" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
