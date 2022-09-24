<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Edit Currency</h4>
      </div>
    </div>

    <div class="row">
      <div class="col-3"></div>
      <div class="col-md-6 px-5 px-md-0">
        <form v-if="currency">
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" v-model="currency.name" required>
          </div>
          <div class="form-group">
            <label>Iso Code</label>
            <input type="text" class="form-control" v-model="currency.isoCode" required>
          </div>
          <div class="form-group">
            <label>USD Conversion Rate</label>
            <input type="number" class="form-control" v-model="currency.usdConversionRate" required>
          </div>
          <button type="button" class="btn btn-primary" @click="editCurrency">Submit</button>
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
      currency: null
    }
  },
  props : ["baseURL", "currencies"],
  methods : {
    async editCurrency() {
      axios.patch(this.baseURL+"currencies/"+this.id, this.currency)
      .then(res => {
        //sending the event to parent to handle
        this.$emit("fetchCurrencies");
        this.$router.push({name : 'AdminCurrency'});
        swal({
          text: "Currency Updated Successfully!",
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
    this.currency = this.currencies.find(currency => currency.id == this.id);
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
