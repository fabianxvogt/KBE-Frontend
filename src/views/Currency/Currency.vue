<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Our Currencies</h4>
        <router-link id="add-Currency" :to="{name : 'AddCurrency'}" v-show="$route.name=='AdminCurrency'">
          <button class="btn">Add a new Currency</button>
        </router-link>
      </div>
    </div>
    <div class="row">
        <div v-for="Currency of Currencies" :key="Currency.id" class="col-md-6 col-xl-4 col-12 pt-3  justify-content-around d-flex">
          <CurrencyBox :Currency="Currency">
          </CurrencyBox>
        </div>
    </div>
  </div>
</template>

<script>
import CurrencyBox from '../../components/Currency/CurrencyBox';
export default {
  name: 'Currency',
  components : {CurrencyBox},
  props : [ "baseURL" , "Currencies" ],
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
