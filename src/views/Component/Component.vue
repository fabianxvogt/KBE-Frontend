<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Our Components</h4>
        <router-link id="add-Component" :to="{name : 'AddComponent'}" v-show="$route.name=='AdminComponent'">
          <button class="btn">Add a new Component</button>
        </router-link>
      </div>
    </div>
    <div class="row">
        <div v-for="Component of Components" :key="Component.id" class="col-md-6 col-xl-4 col-12 pt-3  justify-content-around d-flex">
          <ComponentBox :Component="Component">
          </ComponentBox>
        </div>
    </div>
  </div>
</template>

<script>
import ComponentBox from '../../components/Component/ComponentBox';
export default {
  name: 'Component',
  components : {ComponentBox},
  props : [ "baseURL" , "Components" ],
  mounted(){
    // if (this.$route.name=='AdminComponent' && !localStorage.getItem('token')) {
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

#add-Component {
  float: right;
  font-weight: 500;
}
</style>
