<template><!-- eslint-disable --> 
  <div class="container">
    <h1 class="main-title">{{ msg }}</h1>
    <Block :block="item.titles" :isTitle="isTitle" :handleSort="handleSort" />
    <Block
      v-for="(item, i) in visibleItems"
      :key="item.name"
      :block="item"
      @onEdit="onEdit"
    />
  </div>
</template>
<script>/* eslint-disable */ 
import Block from "./Block";

export default {
  name: "List",
  props: {
    item: {
      type: Object,
      default: "defaultItem"
    }
  },
  data() {
    return {
      isTitle: true,
      isSorted: "none",
      msg: "STAR WARS TABLE",
      visibleItems: this.item.items.map(item => item)
    };
  },
  components: {
    Block
  },
  methods: {
    onEdit(content, type, itemName) {
      this.$emit("onEdit", content, type, itemName);
    },
    handleSort(e) {
      const sortType = e.target.dataset.type;

      if (this.isSorted == "max") {
        this.isSorted = "none";
        return (this.visibleItems = this.item.items.map(item => item));
      }

      if (this.isSorted == "none") {
        this.isSorted = "min";
        const result = this.visibleItems.sort(function(a, b) {
          if (a[sortType] < b[sortType]) {
            return -1;
          }
          if (a[sortType] > b[sortType]) {
            return 1;
          }
          return 0;
        });
        return result;
      }

      if (this.isSorted == "min") {
        this.isSorted = "max";
        const result = this.visibleItems.sort((a, b) => {
          if (a[sortType] > b[sortType]) {
            return -1;
          }
          if (a[sortType] < b[sortType]) {
            return 1;
          }
          return 0;
        });
        return result;
      }

      console.log("result", result);
      console.log("result2", this.item.items);
      this.isSorted = !this.isSorted;
      return result;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main-title {
  text-decoration: underline;
  margin-bottom: 45px;
}
</style>
