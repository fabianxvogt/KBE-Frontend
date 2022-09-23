<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Edit Component</h4>
      </div>
    </div>

    <div class="row">
      <div class="col-3"></div>
      <div class="col-md-6 px-5 px-md-0">
        <form v-if="Component">
          <div class="form-group">
            <label>Category</label>
            <select class="form-control" v-model="Component.categoryId" required>
              <option v-for="category of categories" :key="category.id" :value="category.id">{{category.categoryName}}</option>
            </select>
          </div>
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" v-model="Component.name" required>
          </div>
          <div class="form-group">
            <label>Description</label>
            <input type="text" class="form-control" v-model="Component.description" required>
          </div>
          <div class="form-group">
            <label>ImageURL</label>
            <input type="url" class="form-control" v-model="Component.imageURL" required>
          </div>
          <div class="form-group">
            <label>Price</label>
            <input type="number" class="form-control" v-model="Component.price" required>
          </div>
          <button type="button" class="btn btn-primary" @click="editComponent">Submit</button>
        </form>
      </div>
      <div class="col-3"></div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      Component: null
    }
  },
  props : ["baseURL", "Components", "categories"],
  methods : {
    async editComponent() {
      axios.patch(this.baseURL+"Component/"+this.id, this.Component)
      .then(res => {
        //sending the event to parent to handle
        this.$emit("fetchData");
        this.$router.push({name : 'AdminComponent'});
        swal({
          text: "Component Updated Successfully!",
          icon: "success",
          closeOnClickOutside: false,
        });
      })
      .catch(err => console.log("err", err));
    }
  },
  mounted() {
    // if (!localStorage.getItem('token')) {
    //   this.$router.push({name : 'Signin'});
    //   return;
    // }
    this.id = this.$route.params.id;
    this.Component = this.Components.find(Component => Component.id == this.id);
  }
}
</script>

<style scoped>
h4 {
  font-family: 'Roboto', sans-serif;
  color: #484848;
  font-weight: 700;
}

</style>
