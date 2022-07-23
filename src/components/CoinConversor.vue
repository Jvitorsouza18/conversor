<template>
  <div class="conversor">
    <h2>{{coinA}} to  {{coinB}}</h2>
    <input type="text" v-model="coinAValue" v-bind:placeholder="coinA"/>
    <input type="button" value="Convert" v-on:click="convert">
    <h2>{{coinBvalue}}</h2>
  </div>
</template>

<script>
  export default{
    name:'CoinConversor',
    props: ['coinA', 'coinB'],
    data(){
      return {
        coinAValue: "",
        coinBValue: 0,
      }
    },
    methods: {
      convert() {

        const fromTo = this.coinA + "_" + this.coinB;
        const url = "http://free.currencyconverterapi.com/api/v5/convert?q="
        + fromTo
        + "&compact=y";

        fetch(url).then(res => { return res.json() }).then(json => {
          const rate = json[fromTo].val;
          this.coinBValue = (parseFloat(this.coinAValue) * rate).toFixed(2);
        })
      }
    }
  }

</script>

<style scoped>

.conversor {
  padding: 20px;
}

</style>