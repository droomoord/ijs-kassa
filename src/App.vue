<template>
  <div id="app">
    <loading v-if="loading"> </loading>
    <modal v-if="modal" @quit="modal = false">
      <div>
        <input type="number" v-model="totaal" />
      </div>
      <strong>{{ pin ? "pin" : "contant" }}</strong>

      <div class="afslaan-buttons">
        <div class="afslaan-groen" @click="verstuur">OK</div>
        <div class="afslaan-rood" @click="modal = false">Cancel</div>
      </div>
    </modal>
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
    <div class="afslaan" v-if="bol1 || bol2 || bol3">
      <span>Afslaan:</span>
      <div>
        <a href="#" @click="afslaan(true)">PIN</a>
        <a href="#" @click="afslaan(false)">Contant</a>
      </div>
    </div>
    <div class="totaal">Totaal: {{ totaalAfgerond }}</div>
    <a href="#" v-if="bol1 || bol2 || bol3" class="reset" @click="reset"
      >Reset</a
    >
  </div>
</template>

<script>
import axios from "axios";
import modal from "./components/modal.vue";
import loading from "./components/loading.vue";
export default {
  name: "App",
  components: { modal, loading },
  data() {
    return {
      bol1: 0,
      bol2: 0,
      bol3: 0,
      totaal: 0,
      modal: false,
      pin: Boolean,
      loading: false,
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
          this.totaal += 2.8;
          this.bol2++;
          break;
        case 3:
          this.totaal += 3.8;
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
            this.totaal -= 2.8;
            this.bol2--;
          }

          break;
        case 3:
          if (this.totaal > 0 && this.bol3 > 0) {
            this.totaal -= 3.8;
            this.bol3--;
          }

          break;

        default:
          break;
      }
    },
    reset() {
      this.bol1 = 0;
      this.bol2 = 0;
      this.bol3 = 0;
      this.totaal = 0;
    },
    afslaan(pin) {
      if (pin) this.pin = true;
      else this.pin = false;
      this.modal = true;
    },

    verstuur: async function() {
      console.log("-----------------------");

      console.log(this.bol1);
      console.log(this.bol2);
      console.log(this.bol3);
      console.log(this.totaalAfgerond);
      console.log(this.pin);
      console.log("-----------------------");

      try {
        this.loading = true;

        await axios.post(
          // "http://localhost:3000/sale",
          "/sale",
          {
            products: {
              bol1: this.bol1,
              bol2: this.bol2,
              bol3: this.bol3,
            },
            pin: this.pin,
            total: this.totaalAfgerond,
          }
        );
        this.loading = false;
        this.modal = false;
        this.reset();
      } catch (error) {
        console.log(error);
        this.loading = false;
      }
    },
  },
  computed: {
    totaalAfgerond() {
      return parseFloat(this.totaal).toFixed(2);
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
  z-index: -1;
}
.afslaan {
  position: fixed;
  bottom: 100px;
  left: 50vw;
  display: flex;
  align-items: center;
  gap: 10px;
}
.afslaan div {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.afslaan div * {
  border: 1px solid black;
  padding: 10px;
}
.afslaan-buttons {
  display: flex;
  gap: 20px;
}
.afslaan-groen {
  color: rgb(0, 0, 0);
  border: 1px solid rgb(0, 52, 0);
  background-color: green;
  padding: 10px;
}
.afslaan-rood {
  color: rgb(0, 0, 0);
  border: 1px solid rgb(70, 1, 1);
  background-color: rgb(193, 0, 0);
  padding: 10px;
}
.reset {
  position: fixed;
  bottom: 0;
  left: 0;
  padding: 10px;
  border: 1px solid black;
}
</style>
