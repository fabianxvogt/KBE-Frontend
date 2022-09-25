<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Our ProductComponents</h4>
        <router-link id="add-ProductComponent" :to="{name : 'AddProductComponent'}" v-show="$route.name=='AdminProductComponent'">
          <button class="btn">Add a new ProductComponent</button>
        </router-link>
      </div>
    </div>
    <div class="row">
        <div v-for="ProductComponent of components" :key="ProductComponent.id" class="col-md-6 col-xl-4 col-12 pt-3  justify-content-around d-flex">
          <ProductComponentBox :ProductComponent="ProductComponent">
          </ProductComponentBox>
        </div>
    </div>
  </div>
</template>

<script>
import ProductComponentBox from '../../components/ProductComponent/ProductComponentBox';
export default {
  name: 'ProductComponent',
  components : {ProductComponentBox},
  props : [ "baseURL" , "components" ],
  mounted(){
    // if (this.$route.name=='AdminProductComponent' && !localStorage.getItem('token')) {
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

#add-ProductComponent {
  float: right;
  font-weight: 500;
}
</style>
