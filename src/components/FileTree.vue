<template>
  <ul v-if="tree" class="folders">
    <li>Folders</li>
    <DirectoryElement :directory="tree"></DirectoryElement>
  </ul>
<!--  <div>-->
<!--    <DirectoryElement v-if="isDirectory" :directory="tree">-->
<!--      {{ tree.name }}-->
<!--    </DirectoryElement>-->
<!--  </div>-->
</template>

<script>
const filePath = "../../static/node_modules.json"
import DirectoryElement from "./tree_elements/DirectoryElement"

export default {
  name: "FileTree",
  components: {
    // 'DirectoryElement': () => import('./tree_elements/DirectoryElement')
    DirectoryElement
  },
  data() {
    return {
      tree: ""
    }
  },
  async created() {
    try {
      const response = await fetch(filePath);
      this.tree = await response.json();
    } catch (e) {
      alert(`Error: ${e}`)
    }
  },
  computed: {
    isDirectory() {
      return this.tree.type === "directory";
    }
  },
  methods: {}
}
</script>

<style scoped>
ul.folders {
  padding: 1rem;
  margin: 0;
  box-sizing: border-box;
  width: 100%;
  list-style: none
}
ul.folders > li:first-child {
  padding: 1rem 1rem 1rem 0
}
</style>