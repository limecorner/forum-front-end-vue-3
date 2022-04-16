<template>
  <div class="container py-5">
    <NavTabs />
    <!-- 餐廳類別標籤 RestaurantsNavPills -->
    <RestaurantsNavPills :categories="categories" />

    <div class="row">
      <!-- 餐廳卡片 RestaurantCard-->
      <RestaurantCard
        v-for="restaurant in restaurants"
        :key="restaurant.id"
        :initial-restaurant="restaurant"
      />
    </div>

    <!-- 分頁標籤 RestaurantPagination -->
    <RestaurantsPagination
      :category-id="categoryId"
      :current-page="currentPage"
      :total-page="totalPage"
      :prev="prev"
      :next="next"
    />
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
import RestaurantCard from "../components/RestaurantCard.vue";
import RestaurantsNavPills from "../components/RestaurantsNavPills.vue";
import RestaurantsPagination from "../components/RestaurantsPagination.vue";

const dummyData = {
  restaurants: [
    {
      id: 1,
      name: "Dayne Abbott",
      tel: "1-134-100-1041 x5565",
      address: "4616 Arne Spur",
      opening_hours: "08:00",
      description: "officiis labore et",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=50.81432176695857",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 2,
      name: "Michaela Mohr III",
      tel: "514-067-2564 x5131",
      address: "66692 Jed Lights",
      opening_hours: "08:00",
      description: "dolorem quia magni",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=67.3432858600479",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 3,
      name: "Murray Wehner",
      tel: "1-024-099-9041",
      address: "7481 Rosario Knoll",
      opening_hours: "08:00",
      description: "Ad vero fuga molestias velit ut expedita id accusa",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=13.069129228942744",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 4,
      name: "Joshua Weber",
      tel: "424-024-2249 x96905",
      address: "163 Edythe Freeway",
      opening_hours: "08:00",
      description: "amet",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=6.0287430229847505",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 5,
      name: "Kaitlyn Willms",
      tel: "169.342.7095 x4059",
      address: "78024 Consuelo Light",
      opening_hours: "08:00",
      description: "Provident eum possimus eum nobis. Quo fugiat amet ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=46.65384076641024",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 6,
      name: "Lew Abernathy",
      tel: "(739) 673-7188 x26411",
      address: "6801 Becker Lakes",
      opening_hours: "08:00",
      description: "Quis aut sed eos ipsa minus odio.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=86.87143591840167",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 7,
      name: "Will Leuschke DDS",
      tel: "453.676.5196 x8125",
      address: "5038 Hane Extension",
      opening_hours: "08:00",
      description: "Eius aut qui earum corporis est eum laborum hic. A",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=52.875618597477384",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 8,
      name: "Jayce Emard",
      tel: "(243) 881-8632 x267",
      address: "110 Jamel Shores",
      opening_hours: "08:00",
      description: "Illo occaecati modi adipisci aut fugit necessitati",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=93.7227022029238",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 9,
      name: "Pat Kautzer II",
      tel: "1-058-401-6013",
      address: "155 Delaney Circle",
      opening_hours: "08:00",
      description: "Consectetur voluptates eveniet molestiae aliquid n",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=90.32280459910926",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 10,
      name: "Dominique Harber",
      tel: "314-404-7110 x676",
      address: "6598 Kyra Mountains",
      opening_hours: "08:00",
      description: "quidem",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=47.97045480997737",
      viewCounts: 0,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
  ],
  categories: [
    {
      id: 1,
      name: "中式料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 2,
      name: "日本料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 3,
      name: "義大利料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 5,
      name: "素食料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 6,
      name: "美式料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    {
      id: 7,
      name: "複合式料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
  ],
  categoryId: "",
  page: 1,
  totalPage: [1, 2, 3, 4, 5],
  prev: 1,
  next: 2,
};

export default {
  components: {
    NavTabs,
    RestaurantsNavPills,
    RestaurantCard,
    RestaurantsPagination,
  },
  data() {
    return {
      restaurants: [],
      categories: [],
      categoryId: -1,
      currentPage: 1,
      totalPage: [],
      prev: -1,
      next: -1,
    };
  },
  created() {
    this.fetchRestaurants();
  },
  methods: {
    fetchRestaurants() {
      const {
        restaurants,
        categories,
        categoryId,
        page,
        totalPage,
        prev,
        next,
      } = dummyData;
      this.restaurants = restaurants;
      this.categories = categories;
      this.categoryId = categoryId;
      this.currentPage = page;
      this.totalPage = totalPage;
      this.prev = prev;
      this.next = next;
    },
  },
};
</script>