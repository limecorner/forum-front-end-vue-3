<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ favoritedRestaurants.length }}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="favoritedRestaurant in favoritedRestaurants"
        :key="favoritedRestaurant.id"
        :to="{ name: 'restaurant', params: { id: favoritedRestaurant.id } }"
        class="mr-1"
      >
        <img
          :src="favoritedRestaurant.image"
          width="60"
          height="60"
          class="avatar"
        />
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialFavoritedRestaurants: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      favoritedRestaurants: [],
    };
  },
  created() {
    this.fetchFavoritedRestaurants();
  },
  methods: {
    fetchFavoritedRestaurants() {
      this.favoritedRestaurants = this.initialFavoritedRestaurants;
    },
  },
};
</script>