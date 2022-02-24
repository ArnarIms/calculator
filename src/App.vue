<template>
  <div class="container">
    <div class="row">
      <div class="col"></div>
      <div class="col-6">
        <h1>Welcome to the greatest currency converter ever made!</h1>
        <br />
        <div class="backlogbuttons">
          <button @click="showBacklog = false" class="btn">
            hide your memory
          </button>
          &nbsp;
          <button @click="showBacklog = true" class="btn">
            view your memory
          </button>
        </div>
        <div class="back" v-if="showBacklog">
          <div class="backs">
            <div class="text backlog">
              <ul>
                <li> Hér átti listinn að koma. reyndi en það fór allt í hakk</li>
              </ul>
            </div>
          </div>
        </div>
        <br />
        <div class="card" style="width: 40rem">
          <div class="card-body">
            <h5 class="card-title">Your currency is </h5>
            <h5 class="card-placeholder">
              <conversion v-if="currencys" :convertRate="amounts" :convertAmount="userAmount"/>
            </h5>
          </div>
        </div>
        <br />
        <div class="text">
          <span>
            Pick a bank of your choosing
            <div
              class="btn-group" role="group" aria-label="Basic example" v-for="a in banks" :key="a.id">
              <button
                type="button" class="btn btn2 btn-secondary" @click="setBank(a.name)">
                {{ a.name }}
              </button>
            </div> </span
          ><br /><br />
          <div>
            <Currency :curr="currencys" v-on:amounts="selectedvalue($event)" />
          </div>
          <br /><br />

          <input class="input" type="number" placeholder="" v-model="userAmount"/>
          <span
            ><button @click="addCurrency()" class="btn"> Add to memory</button></span>
        </div>
      </div>
      <div class="col"></div>
    </div>
  </div>
</template>

<script>
import Currency from "./components/currency.vue";
import Conversion from "./components/conversion.vue";

const axios = require("axios").default;
export default {
  name: "App",

  components: {
    Conversion,
    Currency,
  },
  data: function () {
    return {
      banks: [
        { id: "M5", name: "M5" },
        { id: "LB", name: "LB" },
        { id: "Arion", name: "Arion" },
      ],
     
      userAmount: null,
      amounts: [],
      currencys: [],
      viewCurrencys: {},
      selected: [""],
      /*newCurrencys: {
        askValue: "",
        bidValue: "",
        changeCur: "",
        changeper: "",
        longName: "",
      },*/
      showBacklog: false,
      backlog: "",
      API: "https://apis.is/currency/",
    };
  },
  methods: {
    getcurrencyapi: function () {
      axios.get(this.API + this.bank).then((ret) => {
        (this.currencys = ret.data.results), console.log(this.currencys);
      });
    },
    setBank: function (choice) {
      this.bank = choice;
      this.getcurrencyapi();
    },
    selectedvalue: function (selected) {
      this.amounts = selected;
    },
    //addCurrency() {
      //this.selectedvalue.push(this.newCurrencys);
   // },
    
    /*seeCurrency(currencys) {
      this.viewCurrencys = [];
      this.viewCurrencys.push(currencys);
      console.log("view", this.viewCurrencys);
    },*/

    mounted: function () {
      this.getcurrencyapi();
    },
  },
};
</script>

<style>
h1{
  color: red;
  margin-top: 5rem;
}
.card {
  height: 15rem;
  background: blue;
  color: red;
  text-align: center;
}
.card-placeholder {
  font-size: 40px;
}
body {
  background: black;
}
.text {
  color: red;
}
button {
  margin: 20px;
}
.btn{
  color: red;
  background: blue;
}
</style>
