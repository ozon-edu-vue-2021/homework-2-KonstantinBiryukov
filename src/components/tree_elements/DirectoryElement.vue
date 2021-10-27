<template>
  <div class="directory">
    <div>
      <li class="folder" :class="[directoryCopy.contents ? 'is-leaf' : 'is-folder']">
        <span @click="expand()">{{ directoryCopy.name }}</span>

        <ul v-show="directoryCopy.expanded" class="sub-folders" v-if="isContentExists">
          <DirectoryElement v-for="(child, index) in directoryCopy.contents" :directory="child" v-bind:key="index"/>
        </ul>
        <div class="folder-empty" v-else v-show="isContentEmptyAndExpanded">No Data</div>
      </li>
      <!--      <slot></slot>-->
    </div>
  </div>
</template>

<script>
export default {
  name: "DirectoryElement",
  props: {
    directory: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      directoryCopy: ""
    }
  },
  created() {
    this.directoryCopy = {...this.directory}
    this.directoryCopy.expanded = false;
  },
  computed: {
    isContentExists() {
      return this.directoryCopy.contents && this.directoryCopy.contents.length > 0;
    },
    isContentEmptyAndExpanded() {
      return !this.directoryCopy.contents && this.directoryCopy.expanded;
    }
  },
  methods: {
    expand() {
      if (!this.directoryCopy.contents || this.directoryCopy.contents.length === 0) {
        return;
      }
      this.directoryCopy.expanded = !this.directoryCopy.expanded;
      console.log(this.directoryCopy)
    }
  },
}
</script>

<style scoped>
.directory {
  border: 1px dashed black;
}

li.is-folder {
  padding: 1rem;
  border-left: 1px solid #d3d3d3;
  margin-bottom: 0.5rem
}

li.is-folder > span {
  padding: 0.5rem;
  border: 1px solid #d3d3d3;
  cursor: pointer;
  display: inline-block
}

li.is-leaf {
  padding: 0 0 0 1rem;
  color: #000;
}

ul.sub-folders {
  padding: 1rem 1rem 0 0;
  margin: 0;
  box-sizing: border-box;
  width: 100%;
  list-style: none
}

div.folder-empty {
  padding: 1rem 1rem 0 1rem;
  color: #000;
  opacity: 0.5
}

</style>