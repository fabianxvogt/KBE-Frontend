<template>
  <Navbar
    :cartCount="cartCount"
    @resetCartCount="resetCartCount"
    v-if="!['Signup', 'Signin'].includes($route.name)"
  />
  <div style="min-height: 60vh">
    <router-view
      v-if="products && categories"
      :baseURL="baseURL"
      :products="products"
      :categories="categories"
      @fetchData="fetchData"
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
      baseURL: 'https://limitless-lake-55070.herokuapp.com/', // URL from the demo project
      serviceURL: "https://secure-caverns-35338.herokuapp.com/", // Our URL
      products: null,
      categories: null,
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
        .get(this.serviceURL + 'product/')          // For some reason this throws an error. 
        .then((res) => (this.products = res.data )) // It works with the old demo project URL (this.baseURL)
        .catch((err) => console.log(err) );         // but not with ours (this.serviceURL)
      
      this.products = []    // set to empty array to avoid error
      //fetch categories
      await axios   
        .get(this.serviceURL + 'category/')          // Same behaviour for the categories
        .then((res) => (this.categories = res.data))
        .catch((err) => console.log(err));

      this.categories = []
      //fetch cart items
      if (this.token) {
        await axios.get(`${this.serviceURL}cart/?token=${this.token}`).then(
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
    resetCartCount() {
      this.cartCount = 0;
    },
  },
  mounted() {
    this.token = localStorage.getItem('token');
    this.fetchData();
  },
};
</script>

<style>
html {
  overflow-y: scroll;
}
</style>
