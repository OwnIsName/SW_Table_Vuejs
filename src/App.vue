
<template>
  <div id="app">
    <List :item="obj" @onEdit="onEdit" />
    <Popup
      v-if="isClicked"
      @onClose="onClose"
      @onSave="onSave"
      :content="currentItem.content"
    />
  </div>
</template>

<script>/* eslint-disable */ 
import db from "./db/db";
import List from "./components/List";
import Popup from "./components/Popup";

export default {
  name: "App",
  data: () => ({
    obj: db,
    isClicked: false,
    currentItem: {}
  }),
  components: {
    List,
    Popup
  },
  methods: {
    onClose() {
      return (this.isClicked = !this.isClicked);
    },
    onEdit(content, type, itemName) {
      this.currentItem = Object.assign(
        {},
        {
          content: content,
          type: type,
          itemName: itemName
        }
      );
      this.isClicked = !this.isClicked;
    },

    onSave(value) {
      let currentItem = this.obj.items.find(
        item => item.name === this.currentItem.itemName
      );
      currentItem[this.currentItem.type] = value;
      this.isClicked = !this.isClicked;
      this.currentItem = {};
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
