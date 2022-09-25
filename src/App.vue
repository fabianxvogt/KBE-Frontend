<template>
  <Navbar
    :cartCount="cartCount"
    :currencies="currencies"
    :selectedCurrency="selectedCurrency"
    @resetCartCount="resetCartCount"
    @changeCurrency="changeCurrency"
    v-if="!['Signup', 'Signin'].includes($route.name)"
  />
  <div style="min-height: 60vh">
    <router-view
      v-if="products && categories"
      :baseURL="baseURL"
      :products="products"
      :categories="categories"
      :currencies="currencies"
      :components="components"
      :selectedCurrency="selectedCurrency"
      @fetchData="fetchData"
      @fetchCurrencies="fetchCurrencies"
      @changeCurrency="changeCurrency"
    >
    </router-view>
  </div>
  <Footer v-if="!['Signup', 'Signin'].includes($route.name)" />
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
export default {
  data() {
    return {
      //baseURL: 'https://limitless-lake-55070.herokuapp.com/', // URL from the demo project
      baseURL: "https://secure-caverns-35338.herokuapp.com/", // Our URL
      products: [],
      categories: [],
      currencies: [],
      components: [],
      selectedCurrency: null,
      key: 0,
      token: null,
      cartCount: 0,
    };
  },

  components: { Footer, Navbar },
  methods: {
    async fetchData() {
      // fetch products
      
      await axios
        .get(this.baseURL + 'product/')          
        .then((res) => (this.products = res.data )) 
        .catch((err) => console.log(err) );         
      
      for (let product of this.products) {

        product.priceLocal = product.price
      }

      //fetch categories
      await axios   
        .get(this.baseURL + 'category/')       
        .then((res) => (this.categories = res.data))
        .catch((err) => console.log(err));

      //fetch cart items
      if (this.token) {
        await axios.get(`${this.baseURL}cart/?token=${this.token}`).then(
          (response) => {
            if (response.status == 200) {
              // update cart
              this.cartCount = Object.keys(response.data.cartItems).length;
            }
          },
          (error) => {
            console.log(error);
          }
        );
      }
    },

    async changeCurrency(currency) {
      this.selectedCurrency = currency
      if (this.selectedCurrency != null) {
          for (let product of this.products) {
              await axios   
              .get(this.baseURL + 'price/product/' + product.id + '?currency='+ this.selectedCurrency.isoCode)       
              .then((res) => (product.priceLocal = res.data.totalPrice))
              .catch((err) => console.log(err));
            //product.priceLocal = product.price / this.selectedCurrency.usdConversionRate
          }
      }
    },
    async fetchCurrencies() {
      await axios
        .get(this.baseURL + 'currencies/')          
        .then((res) => (this.currencies = res.data )) 
        .catch((err) => console.log(err) );         
    },
    async fetchComponents() {
      await axios
        .get(this.baseURL + 'components/')          
        .then((res) => (this.components = res.data )) 
        .catch((err) => console.log(err) );         
    },
    resetCartCount() {
      this.cartCount = 0;
    },
  },
  mounted() {
    this.token = localStorage.getItem('token');
    this.fetchData();
    this.fetchCurrencies();
  },
};
</script>

<style>
html {
  overflow-y: scroll;
}
</style>
