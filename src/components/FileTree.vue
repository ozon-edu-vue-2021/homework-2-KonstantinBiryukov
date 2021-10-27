<template>
  <div>
    <div v-for="node in nodes"
         :key="node.name"
         :style="{'margin-left': `${depth * 15}px`}"
         class="node">

      <span
          class="type expandable"
          v-if="node.contents"
          @click="clickNode(node)">
        {{ isExpanded(node) ? '&#9660;' : '&#9658;' }}
      </span>
      <span v-else class="type not-expandable">
        &#9671;
      </span>

      <span :style="getStyle(node)">{{ node.name }}</span>

      <FileTree
          v-if="isExpanded(node)"
          :nodes="node.contents"
          :depth="depth + 1"/>
    </div>
  </div>
</template>

<script>
export default {
  name: "FileTree",
  props: {
    nodes: Array,
    depth: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      expanded: [],
    };
  },
  methods: {
    isExpanded(node) {
      return this.expanded.indexOf(node) !== -1;
    },
    clickNode(node) {
      (!this.isExpanded(node)) ?
          this.expanded.push(node) :
          this.expanded.splice(this.expanded.indexOf(node));
    },
    getStyle(node) {
      let color = "yellow";
      if (!node.contents) {
        switch (node.type) {
          case "link":
            color = "white";
            break;
          case "file":
            color = "red";
            break;
        }
      }
      return {color};
    },
  },
};
</script>

<style scoped>
.node {
  text-align: left;
  font-size: 18px;
}

.type {
  margin-right: 10px;
}

.expandable {
  cursor: grab;
}

.not-expandable {
  cursor: not-allowed;
}
</style>
