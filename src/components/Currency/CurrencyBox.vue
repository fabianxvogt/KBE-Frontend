<template>  
  <div class="card h-100 w-100" style="align-content:center">
    <div class="card-body">
      <router-link :to="{ name: 'ShowCurrencyDetails', params: { id: currency.id } }" style="width: 200px;">
        <h5 class="card-title">{{ currency.name }}</h5>
      </router-link>
      <div style="width: 100px;">
        {{ currency.isoCode }}
      </div>
      <div style="width: 200px;">
        {{ currency.usdConversionRate }}
      </div>
      <router-link
        id="edit-currency"
        :to="{ name: 'EditCurrency', params: { id: currency.id } }"
        v-show="$route.name == 'AdminCurrency'" 
        style="width: 100px;"
      >
        Edit
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrencyBox",
  props: ["currency"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowCurrencyDetails",
        params: { id: this.currency.id },
      });
    },
  },
};
</script>

<style scoped>
.embed-responsive .card-img-top {
  object-fit: cover;
}

a {
  text-decoration: none;
  padding:0
}


.card-title {
  color: #484848;
  font-size: 1.1rem;
  font-weight: 400;
  margin: 0;
}

.card-title:hover {
  font-weight: bold;
}

.card-body {
  padding: 10px 40px 10px 40px;
  font-size: 1rem;
  display: flex; 
  flex-direction:row; 
  border: 1px solid black; 
  justify-content: space-between; 
}

#edit-Currency {
  float: right;
}
</style>
