<template>
  <div class="backdrop">
    <div class="modal">
      <div class="quit" @click="quit">X</div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  methods: {
    quit() {
      this.$emit("quit");
    },
  },
};
</script>

<style scoped>
.backdrop {
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(74, 74, 74, 0.632);
}
.modal {
  position: fixed;
  top: 10vh;
  left: 5vw;
  width: 90vw;
  height: 40vh;
  background-color: white;
  border-radius: 5px;
  border: 1px solid black;
  z-index: 100;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;

  font-size: 1.3em;
}
.quit {
  position: absolute;
  top: 0;
  right: 0;
  padding: 10px;
  border: 1px solid black;
}
</style>
