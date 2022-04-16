<template>
  <div class="container py-5">
    <h1>餐廳描述頁</h1>
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantDetail :initial-restaurant="restaurant" />
    <!-- <RestaurantDashboard :restaurant="restaurant" v-if="false" /> -->
    <hr />
    <!-- 餐廳評論 RestaurantComments -->
    <RestaurantComments
      :restaurant-comments="restaurantComments"
      @after-delete-comment="afterDeleteComment"
    />
    <!-- 新增評論 CreateComment -->
    <CreateComment
      :restaurant-id="restaurant.id"
      @after-create-comment="afterCreateComment"
    />
  </div>
</template>

<script>
import RestaurantDetail from "../components/RestaurantDetail.vue";
import RestaurantComments from "../components/RestaurantComments.vue";
import CreateComment from "../components/CreateComment.vue";
// import RestaurantDashboard from "../components/RestaurantDashboard.vue";

const dummyData = {
  restaurant: {
    id: 1,
    name: "Dayne Abbott",
    tel: "1-134-100-1041 x5565",
    address: "4616 Arne Spur",
    opening_hours: "08:00",
    description: "officiis labore et",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=50.81432176695857",
    viewCounts: 1,
    createdAt: "2022-03-11T06:14:36.000Z",
    updatedAt: "2022-04-14T14:28:04.781Z",
    CategoryId: 3,
    Category: {
      id: 3,
      name: "義大利料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
    FavoritedUsers: [],
    LikedUsers: [],
    Comments: [
      {
        id: 1,
        text: "Dolores numquam est numquam optio sit.",
        UserId: 1,
        RestaurantId: 1,
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$dEj2FuoeieIlkN.GJfoC9O.SwoaY99MfXet4z8vB5wAf12Vwa5NjS",
          isAdmin: true,
          image: null,
          createdAt: "2022-03-11T06:14:36.000Z",
          updatedAt: "2022-03-11T06:14:36.000Z",
        },
      },
      {
        id: 101,
        text: "Consequatur consequatur aperiam laborum voluptas.",
        UserId: 2,
        RestaurantId: 1,
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
        User: {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$bX6prwanTs8SK6l/74g3UOWAbGURSxcrmvZlCjsFKBfOtz.P6nhba",
          isAdmin: false,
          image: null,
          createdAt: "2022-03-11T06:14:36.000Z",
          updatedAt: "2022-03-11T06:14:36.000Z",
        },
      },
      {
        id: 51,
        text: "Omnis est adipisci illum vitae.",
        UserId: 3,
        RestaurantId: 1,
        createdAt: "2022-03-11T06:14:36.000Z",
        updatedAt: "2022-03-11T06:14:36.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$yRfxRHfliQKntt5GnMdxb.OCB38jf3IFjnnP6Yj180JPqmqD2.URC",
          isAdmin: false,
          image: null,
          createdAt: "2022-03-11T06:14:36.000Z",
          updatedAt: "2022-03-11T06:14:36.000Z",
        },
      },
    ],
  },
  isFavorited: false,
  isLiked: false,
};
const dummyUser = {
  currentUser: {
    id: 1,
    name: "root",
    email: "root@example.com",
    image: null,
    isAdmin: true,
  },
  isAuthenticated: true,
};

export default {
  components: {
    RestaurantDetail,
    RestaurantComments,
    CreateComment,
    // RestaurantDashboard,
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryName: "",
        image: "",
        openingHours: "",
        tel: "",
        address: "",
        description: "",
        isFavorited: false,
        isLiked: false,
      },
      restaurantComments: [],
      currentUser: {},
    };
  },
  created() {
    const id = this.$route.params;
    console.log("params", id);
    this.fetchRestaurant(id);
    this.currentUser = dummyUser.currentUser;
  },
  methods: {
    fetchRestaurant(restaurantId) {
      console.log("fetchRestaurant id: ", restaurantId);
      this.restaurant = {
        id: dummyData.restaurant.id,
        name: dummyData.restaurant.name,
        categoryName: dummyData.restaurant.Category.name,
        image: dummyData.restaurant.image,
        openingHours: dummyData.restaurant.opening_hours,
        tel: dummyData.restaurant.tel,
        address: dummyData.restaurant.address,
        description: dummyData.restaurant.description,
        isFavorited: dummyData.isFavorited,
        isLiked: dummyData.isLiked,
      };
      this.restaurantComments = dummyData.restaurant.Comments;
    },
    afterDeleteComment(commentId) {
      // console.log("afterDeleteComment", commentId);

      this.restaurantComments = this.restaurantComments.filter(
        (comment) => comment.id !== commentId
      );
    },
    afterCreateComment(payload) {
      console.log("payload", payload);
      const { commentId, restaurantId, text } = payload;
      this.restaurantComments.push({
        id: commentId,
        User: { name: this.currentUser.name, id: this.currentUser.id },
        RestaurantId: restaurantId,
        text,
        createdAt: new Date(),
      });
    },
  },
};
</script>