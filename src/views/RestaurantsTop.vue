<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <div
      v-for="restaurant in restaurants"
      :key="restaurant.id"
      class="card mb-3"
      style="max-width: 540px; margin: auto"
    >
      <div class="row no-gutters">
        <div class="col-md-4">
          <router-link
            :to="{ name: 'restaurant', params: { id: restaurant.id } }"
          >
            <img class="card-img" :src="restaurant.image" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ restaurant.name }}</h5>
            <span class="badge badge-secondary"
              >收藏數：{{ restaurant.FavoriteCount }}</span
            >
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <router-link
              :to="{ name: 'restaurant', params: { id: restaurant.id } }"
              class="btn btn-primary mr-2"
              >Show</router-link
            >

            <button
              v-if="restaurant.isFavorited"
              @click.stop.prevent="onRemoveFromFavorite(restaurant)"
              type="button"
              class="btn btn-danger mr-2"
            >
              移除最愛
            </button>
            <button
              v-else
              @click.stop.prevent="onAddToFavorite(restaurant)"
              type="button"
              class="btn btn-primary"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
const dummyData = {
  restaurants: [
    {
      id: 50,
      name: "Wilbert Donnelly",
      tel: "936-101-3145 x46375",
      address: "57890 Jenkins Spring",
      opening_hours: "08:00",
      description: "Sequi doloribus minus est sed doloremque quaerat. ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=28.06596604246718",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 49,
      name: "Mr. Jazmyn Boehm",
      tel: "595.522.0044 x6012",
      address: "5283 Pacocha Mountain",
      opening_hours: "08:00",
      description: "Dolores id dolores.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=76.41242000222897",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 2,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 48,
      name: "Evans Roberts",
      tel: "236-524-0581",
      address: "607 Janick Fall",
      opening_hours: "08:00",
      description: "Asperiores aut explicabo soluta voluptatem quis nu",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=42.16788517553069",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 47,
      name: "Anita Heaney",
      tel: "1-402-038-5895 x08763",
      address: "19913 Greenfelder Ramp",
      opening_hours: "08:00",
      description: "aut accusantium eum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=85.79014872688889",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 1,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 46,
      name: "Gordon Hansen",
      tel: "836.891.4846 x29078",
      address: "31834 Stehr Stravenue",
      opening_hours: "08:00",
      description: "facere dolores ut",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=70.08310217328886",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 1,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 45,
      name: "Chance Schinner",
      tel: "1-668-593-9494",
      address: "7883 Robel River",
      opening_hours: "08:00",
      description: "Et animi impedit illo eum aut.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=51.08824140995265",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 44,
      name: "Erin Von",
      tel: "1-678-118-8811",
      address: "25257 Runte Rue",
      opening_hours: "08:00",
      description: "libero",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=71.3357759663752",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 43,
      name: "Jolie Pacocha",
      tel: "314.995.7955 x11911",
      address: "272 Claudine Expressway",
      opening_hours: "08:00",
      description: "Mollitia neque ab ab saepe voluptates in ut et nul",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=87.70301289810996",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 4,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 42,
      name: "Gregg Carter",
      tel: "073-562-5671 x516",
      address: "85301 Lind Keys",
      opening_hours: "08:00",
      description: "accusamus",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=99.08495423828457",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 5,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
    {
      id: 41,
      name: "Vince Harvey",
      tel: "549-257-3341",
      address: "22758 Ford Island",
      opening_hours: "08:00",
      description: "Vitae occaecati totam saepe culpa est dignissimos ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=73.16169638627655",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 1,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
  ],
};
export default {
  name: "RestaurantsTop",
  components: {
    NavTabs,
  },
  data() {
    return {
      restaurants: dummyData.restaurants,
    };
  },
  methods: {
    onAddToFavorite(restaurant) {
      this.restaurants = this.restaurants.map((_restaurant) => {
        if (_restaurant.id === restaurant.id) {
          return {
            ..._restaurant,
            isFavorited: true,
          };
        } else {
          return _restaurant;
        }
      });
    },
    onRemoveFromFavorite(restaurant) {
      this.restaurants = this.restaurants.map((_restaurant) => {
        if (_restaurant.id === restaurant.id) {
          return {
            ..._restaurant,
            isFavorited: false,
          };
        } else {
          return {
            ..._restaurant,
          };
        }
      });
    },
  },
};
</script>