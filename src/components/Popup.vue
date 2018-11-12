<template>
  <div class="container" @click="onClose">
    <button class="close-button">X</button>
    <div class="wrapper">
      <form action="" class="popup-form">
        <input type="text" :value="content" class="text-field" />
        <button class="save-button" @click.prevent="onSave">Save</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Popup",
  methods: {
    onClose(e) {
      const targetClass = e.target.getAttribute("class");
      if (targetClass == "container" || targetClass == "close-button") {
        this.$emit("onClose");
      }
    },
    onSave(e) {
      const value = document.querySelector(".text-field").value;
      this.$emit("onSave", value);
    }
  },

  props: {
    content: {
      type: String,
      default: ""
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  z-index: 100;
  background-color: rgba(0, 0, 0, 0.8);
}
.wrapper {
  width: 30%;
  height: 200px;
  background-color: antiquewhite;
  box-shadow: 4px 6px 8px 3px rgba(0, 0, 0, 0.75);
}
.close-button {
  position: fixed;
  top: 10%;
  left: 90%;
  width: 50px;
  height: 50px;
  border: 0;
  border-radius: 50%;
  outline: none;
  box-shadow: 4px 6px 33px 3px rgba(0, 0, 0, 0.75);
  font-size: 30px;
  font-weight: bold;
  color: #bbb;
  background-color: rgba(0, 0, 0, 0.75);
}
.close-button:hover {
  color: #eee;
  box-shadow: 4px 6px 8px 3px rgba(0, 0, 0, 0.75);
}

.popup-form {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.text-field {
  padding: 5px;
  height: 20%;
  width: 80%;
  font-size: 20px;
  font-weight: bold;
  color: #2c3e50;
  background-color: rgba(0, 0, 0, 0);
  outline: none;
  border: 0;
  box-shadow: 0px 0px 9px 2px rgba(0, 0, 0, 0.7);
}
.save-button {
  width: 150px;
  height: 50px;
  border: 0;
  border-radius: 10%;
  outline: none;
  box-shadow: 10px 10px 21px 0px rgba(0, 0, 0, 0.75);
  font-size: 30px;
  font-weight: bold;
  color: #777;
}
.save-button:hover {
  box-shadow: 7px 7px 11px -6px rgba(0, 0, 0, 0.75);
}
</style>
