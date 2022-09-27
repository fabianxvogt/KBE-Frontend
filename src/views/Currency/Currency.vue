<template>
  <div class="container" style="justify-content: center; align-items: center;">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Our Currencies</h4>
        <router-link id="add-Currency" :to="{name : 'AddCurrency'}" v-show="$route.name=='AdminCurrency'">
          <button class="btn">Add a new Currency</button>
        </router-link>
      </div>
    </div>
    <div style="display:flex; flex-direction: row;justify-content: center;">
      <div style="display:flex; flex-direction: row;justify-content: center; padding:20px; font-size: larger;">
        <div style="width: 200px;">
          Name
        </div>
        <div style="width: 100px;">
          ISO
        </div>
        <div style="width: 200px;">
          USD Conv. Rate
        </div>
        <div style="width: 100px;">
          Edit
        </div>
      </div>
    </div>
    <div style="display:flex; flex-direction: row; justify-content: center;">
      <div class="currency-table" style="align-self: center; justify-content:center; display: flex; flex-direction: column; margin:0">
        <div v-for="currency of currencies" :key="currency.isoCode" style="padding:0px">
          <CurrencyBox :currency="currency">
          </CurrencyBox>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
import CurrencyBox from '../../components/Currency/CurrencyBox';
export default {
  name: 'Currency',
  components : {CurrencyBox},
  props : [ "baseURL" , "currencies" ],
  mounted(){
    // if (this.$route.name=='AdminCurrency' && !localStorage.getItem('token')) {
    //   this.$router.push({name : 'Signin'});
    // }
  }
}
</script>

<style scoped>
h4 {
  font-family: 'Roboto', sans-serif;
  color: #484848;
  font-weight: 700;
}

#add-Currency {
  float: right;
  font-weight: 500;
}
</style>
