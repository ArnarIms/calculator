<template>
  <div class="text">
    Choose your currency
    <div id="Currency">
      <div class="btn-group" role="group" v-for="name in curr" :key="name.id" v-on:click="isHidden = !isHidden">
        <button type="button" class="btn btn2 btn-secondary" @click="selectC(name)">
          {{name.shortName}}
        </button>
      </div>
      <div class="text" v-if="!isHidden">
      You have picked {{selectedC}} its price by the bank you chose is {{selectedValue.toFixed(2)}} krónur
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Currency",
  props: {
    curr: Array,
  },
  data: () => {
        return {
            selectedC: "",
            selectedValue: 0,
            isHidden: true,
        };
        
    },

    methods: {
        selectC: function(newC) {
            this.selectedC = newC.longName;
            this.selectedValue = newC.value;
            this.$emit("amounts", newC);
        },
        /*created() {
        this.$root.$refs.A = this; Þetta gekk ekki upp hjá mér. Fékk upp currency en ómögulegt að gera eitthvað við þetta.
    },*/
    },
}
</script>

<style>
.btn-group button{
  color: red;
  background: blue;
  margin: 20px;
  margin-top: 20px;
  
}
.text{
  color: red;
  font-size: 20px;
 
}

</style>