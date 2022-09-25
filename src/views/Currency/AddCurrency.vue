<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Add new Currency</h4>
      </div>
    </div>

    <div class="row">
      <div class="col-3"></div>
      <div class="col-md-6 px-5 px-md-0">
        <form>
          <div class="form-group">
            <label>ISO Code</label>
            <input type="text" class="form-control" v-model="isoCode" required>
          </div>          
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" v-model="name" required>
          </div>
          <div class="form-group">
            <label>USD Conversion Rate</label>
            <input type="text" class="form-control" v-model="usdConversionRate" required>
          </div>
          <button type="button" class="btn btn-primary" @click="addCurrency">Submit</button>
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
      isoCode : null,
      name : null,
      usdConversionRate : null
    }
  },
  props : ["baseURL", "currencies"],
  methods : {
    async addCurrency() {
      const newCurrency = {
        isoCode : this.isoCode,
        name : this.name,
        usdConversionRate : this.usdConversionRate
      }

      await axios({
        method: 'post',
        url: this.baseURL+"currencies",
        data : JSON.stringify(newCurrency),
        headers: {
          'Content-Type': 'application/json'
        }
      })
      .then(res => {
        //sending the event to parent to handle
        this.$emit("fetchCurrencies");
        this.$router.push({name : 'AdminCurrency'});
        swal({
          text: "Currency Added Successfully!",
          icon: "success",
          closeOnClickOutside: false,
        });
      })
      .catch(err => console.log(err));
    }
  },
  mounted() {
    // if (!localStorage.getItem('token')) {
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

</style>
