<template>
  <div class="loading">
    LOADING...
  </div>
</template>

<script>
export default {
  name: "loading",
};
</script>

<style>
.loading {
  position: fixed;
  left: 20vw;
  top: 70vh;
  font-weight: bold;
  font-size: 2em;
  padding: 30px;
  background-color: rgb(255, 255, 255);
  z-index: 200;
}
</style>
