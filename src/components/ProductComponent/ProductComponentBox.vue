<template>
  <div class="card h-100 w-100">
    <div class="embed-responsive embed-responsive-16by9">
      <img
        class="card-img-top embed-responsive-item"
        :src="ProductComponent.imageURL"
        alt="ProductComponent Image"
      />
    </div>
    <div class="card-body">
      <router-link :to="{ name: 'ShowDetails', params: { id: ProductComponent.id } }"
        ><h5 class="card-title">{{ ProductComponent.name }}</h5></router-link
      >
      <p class="card-text"><sup>$</sup>{{ ProductComponent.price }}</p>
      <p class="card-text font-italic">
        {{ ProductComponent.description.substring(0, 65) }}...
      </p>
      <router-link
        id="edit-ProductComponent"
        :to="{ name: 'EditProductComponent', params: { id: ProductComponent.id } }"
        v-show="$route.name == 'AdminProductComponent'"
      >
        Edit
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductComponentBox",
  props: ["ProductComponent"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowDetails",
        params: { id: this.ProductComponent.id },
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

#edit-ProductComponent {
  float: right;
}
</style>
