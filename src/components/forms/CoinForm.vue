<template>
  <form @submit.prevent="submitForm">
    <div style="display:flex; justify-content:center; flex-direction:column;">
      <div style="display:flex; justify-content:center; align-items: center;" class="form-control">
        <label style="margin-right: 5px;" for="crypto">Choose a cryptocurrency:</label>
        <select v-model="coin" style="margin-right: 5px;" id="crypto" name="crypto">
          <option :value="{val:'BTC', title:'Bitcoin'}">Bitcoin</option>
          <option :value="{val:'ETC', title: 'Ethereum'}">Ethereum</option>
          <option :value="{val:'XRP', title:'XRP'}">XRP</option>
        </select>
        <base-button>Submit</base-button>
      </div>
      <coin-detail
        v-if="coinDetails.ask"
        :ask="coinDetails.ask"
        :calculatedVal="coinDetails.calculatedVal"
      ></coin-detail>
      <p>Your local storage is set to: {{localCoin.val}}</p>
      <base-button @click="clearLocalStorage">Clear Storage</base-button>
      <p v-if="!formIsValid">Please fix the above errors and submit again.</p>
    </div>
  </form>
</template>

<script>
  import CoinDetail from "../layout/CoinDetail.vue";

export default {

    components:{CoinDetail},
 
    mounted(){
        if(this.coin.val){
        this.getCoin();
        }else {return}
        
    },
  
    
    data(){
        return {
         selected:false,  
          formIsValid: true,  
         
         coinDetails:{
            ask:null,
            calculatedVal:null
          },
            coin:{
              val:'',
              isValid:true,
              title:'',               
        },
            localCoin:{
                val:'',
                title:''
            }
        }
    },

    watch: {
  'coin.val':     function () {
  this.setStorage()
  }   
        
},


    methods:{
      async getCoinInfo(coin){
        let  url = `https://trade.cointree.com/api/prices/aud/${coin}` 
        const response = await fetch(url)
        const responseData = await response.json();
        
        if(!response.ok){
          const error = new Error(responseData.message || 'Failed to Fetch!')
          throw error;
        }
        
       this.coinDetails = {
         ask: responseData.ask,
         calculatedVal: (responseData.bid /responseData.ask) *100 
       } 
       
      },
     
     setStorage(){
            console.log(this.coin.title);
            localStorage.setItem('storedData', JSON.stringify({
            val: this.coin.val,
            title: this.coin.title
        }));
     },

     clearLocalStorage(){
        localStorage.removeItem('storedData');
        this.$router.go();
      },

      getCoin(){
         this.localCoin  = localStorage.getItem('storedData');
         if(this.localCoin){
         this.localCoin = JSON.parse(this.localCoin);
         this.coin= this.localCoin;
         }
      },  

      validateForm(){
        this.formIsValid=true;
        
      },
        submitForm(){
            if(this.coin){
               // this.setStorage();
            }
    
            this.getCoin(); 
            this.getCoinInfo(this.coin.val)     
        }
    }
}
</script>
<style scoped>
.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

h3 {
  margin: 0.5rem 0;
  font-size: 1rem;
}
</style>