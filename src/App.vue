<template>
  <div id="app">
    <div class="buttons">
      <div>
        <button @click="clicked(1)">
          <img class="ijsje" src="./assets/bol1.png" alt="" />
        </button>
        <span class="x" @click="verwijder(1)">X</span>
      </div>
      <div>
        <button @click="clicked(2)">
          <img class="ijsje" src="./assets/bol2.png" alt="" />
        </button>

        <span class="x" @click="verwijder(2)">X</span>
      </div>
      <div>
        <button @click="clicked(3)">
          <img class="ijsje" src="./assets/bol3.png" alt="" />
        </button>
        <span class="x" @click="verwijder(3)">X</span>
      </div>
    </div>
    <div v-if="bol1 > 0">
      {{ bol1 }} x 1 bolletje

      <img
        v-for="index in bol1"
        v-bind:key="index"
        class="ijsje-klein"
        src="./assets/bol1.png"
        alt=""
      />
    </div>
    <div v-if="bol2 > 0">
      {{ bol2 }} x 2 bolletjes
      <img
        v-for="index in bol2"
        v-bind:key="index"
        class="ijsje-klein"
        src="./assets/bol2.png"
        alt=""
      />
    </div>
    <div v-if="bol3 > 0">
      {{ bol3 }} x 3 bolletjes
      <img
        v-for="index in bol3"
        v-bind:key="index"
        class="ijsje-klein"
        src="./assets/bol3.png"
        alt=""
      />
    </div>
    <div class="totaal">Totaal: {{ totaalAfgerond }}</div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      bol1: 0,
      bol2: 0,
      bol3: 0,
      totaal: 0,
    };
  },
  methods: {
    clicked(type) {
      switch (type) {
        case 1:
          this.totaal += 1.8;
          this.bol1++;
          break;
        case 2:
          this.totaal += 2.6;
          this.bol2++;
          break;
        case 3:
          this.totaal += 3.4;
          this.bol3++;
          break;

        default:
          break;
      }
    },
    verwijder(type) {
      switch (type) {
        case 1:
          if (this.totaal > 0 && this.bol1 > 0) {
            this.totaal -= 1.8;
            this.bol1--;
          }
          break;
        case 2:
          if (this.totaal > 0 && this.bol2 > 0) {
            this.totaal -= 2.6;
            this.bol2--;
          }

          break;
        case 3:
          if (this.totaal > 0 && this.bol3 > 0) {
            this.totaal -= 3.4;
            this.bol3--;
          }

          break;

        default:
          break;
      }
    },
  },
  computed: {
    totaalAfgerond() {
      return this.totaal.toFixed(2);
    },
  },
};
</script>

<style>
body {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
.buttons {
  display: flex;
  flex-direction: column;
  height: 50vh;
  margin-bottom: 50px;
}
.buttons > * {
  height: 200px;
}
button {
  width: 70%;
  height: 100%;
  background-color: white;
  border-radius: 10px;
}

.x {
  margin-left: 50px;
  color: red;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  border: 1px solid red;
  border-radius: 50%;
  padding: 5px 10px;
}
.totaal {
  position: fixed;
  bottom: 10px;
  right: 20px;
  font-weight: bold;
  font-size: 1.5em;
}
.ijsje {
  width: 50px;
}
.ijsje-klein {
  width: 20px;
  position: relative;
  top: 15px;
}
</style>
