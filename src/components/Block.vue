<template>
  <div class="container" v-if="isTitle" @click="handleSort">
    <h2 v-for="(item, i) in block" :data-type="i">{{ item }}</h2>
  </div>
  <div class="container" v-else @click="onEdit">
    <h3 v-for="(item, i) in block" :data-type="i">{{ item }}</h3>
  </div>
</template>

<script>
export default {
  name: "Block",

  props: {
    block: {
      type: Object
    },
    isTitle: {
      type: Boolean,
      default: false
    },
    handleSort: {
      type: Function
    }
  },
  methods: {
    onEdit(e) {
      const container = e.currentTarget;
      const itemName = container.firstChild.innerHTML;
      const content = e.target.innerHTML;
      const type = e.target.dataset.type;
      this.$emit("onEdit", content, type, itemName);
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  box-sizing: border-box;
  margin: 0 2%;
  background-color: #aaa;
}
h2,
h3 {
  display: inline-block;
  align-items: center;
  justify-content: center;
  height: 50px;
  flex: 1;
  border: 1px white solid;
  margin: 0;
  padding: 5px;
  flex-wrap: wrap;
}
h2 {
  text-decoration: underline;
}
h3 {
  justify-content: flex-start;
  background-color: #ccc;
}

h3:hover {
  cursor: pointer;
  background-color: #cc7766;
  color: white;
  transition: 0.4s ease-out;
}
h2:hover {
  cursor: pointer;
  background-color: #cc7766;
  color: white;
  transition: 0.4s ease-out;
}
</style>
