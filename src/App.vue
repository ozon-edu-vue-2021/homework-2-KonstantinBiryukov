<template>
  <div id="app">
    <h1>File Tree</h1>
    <FileTree :nodes="root"/>
  </div>
</template>

<script>
import FileTree from "./components/FileTree.vue";
import nodeModules from "../public/static/node_modules.json";

export default {
  name: "app",
  data() {
    return {
      root: nodeModules,
    };
  },
  components: {
    FileTree,
  },
};
</script>

<style>
body {
  background-color: #444;
  color: white;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>