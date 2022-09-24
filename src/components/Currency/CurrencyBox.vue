<template>
  <div class="card h-100 w-100">
    <div class="embed-responsive embed-responsive-16by9">
      <img
        class="card-img-top embed-responsive-item"
        :src="Currency.imageURL"
        alt="Currency Image"
      />
    </div>
    <div class="card-body">
      <router-link :to="{ name: 'ShowDetails', params: { id: Currency.id } }"
        ><h5 class="card-title">{{ Currency.name }}</h5></router-link
      >
      <p class="card-text"><sup>$</sup>{{ Currency.price }}</p>
      <p class="card-text font-italic">
        {{ Currency.description.substring(0, 65) }}...
      </p>
      <router-link
        id="edit-Currency"
        :to="{ name: 'EditCurrency', params: { id: Currency.id } }"
        v-show="$route.name == 'AdminCurrency'"
      >
        Edit
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrencyBox",
  props: ["Currency"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowDetails",
        params: { id: this.Currency.id },
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
}

.card-title {
  color: #484848;
  font-size: 1.1rem;
  font-weight: 400;
}

.card-title:hover {
  font-weight: bold;
}

.card-text {
  font-size: 0.9rem;
}

#edit-Currency {
  float: right;
}
</style>
