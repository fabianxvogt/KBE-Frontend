<template>
  <div class="card h-100 w-100">
    <div class="embed-responsive embed-responsive-16by9">
      <img
        class="card-img-top embed-responsive-item"
        :src="Component.imageURL"
        alt="Component Image"
      />
    </div>
    <div class="card-body">
      <router-link :to="{ name: 'ShowDetails', params: { id: Component.id } }"
        ><h5 class="card-title">{{ Component.name }}</h5></router-link
      >
      <p class="card-text"><sup>$</sup>{{ Component.price }}</p>
      <p class="card-text font-italic">
        {{ Component.description.substring(0, 65) }}...
      </p>
      <router-link
        id="edit-Component"
        :to="{ name: 'EditComponent', params: { id: Component.id } }"
        v-show="$route.name == 'AdminComponent'"
      >
        Edit
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComponentBox",
  props: ["Component"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowDetails",
        params: { id: this.Component.id },
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

#edit-Component {
  float: right;
}
</style>
