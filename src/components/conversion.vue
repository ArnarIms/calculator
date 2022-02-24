<template>
    <div>
            {{(convertAmount * convertRate.value).toFixed(0)}} Krónur
        
    </div>
</template>

<script>
export default {
    props: {
        convertAmount:Boolean,
        convertRate:Boolean,
    },
    
     data: () => {
    
        return {
            convertAmount: 0,
            convertRate: 0,
        };
        
},
//methods:{
    //getAmount(){
      // Amounted = convertAmount * convertRate.value;
      //  if (getAmount(Amount){
      //   !== "undefined" || Amount !=== null)},
  //  }

};


</script>

<style>

</style>
