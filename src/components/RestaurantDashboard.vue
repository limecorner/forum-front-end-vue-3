<template>
  <div class="container py-5">
    <div>
      <h1>{{ restaurant.name }}</h1>
      <span class="badge badge-secondary mt-1 mb-3">
        {{ restaurant.Category.name }}
      </span>
    </div>

    <hr />

    <ul>
      <li>評論數： {{ restaurant.Comments.length }}</li>
      <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
    </ul>

    <button type="button" class="btn btn-link" @click="$router.back()">
      回上一頁
    </button>
  </div>
</template>

<script>
const dummyRestaurant = {
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
    updatedAt: "2022-04-14T14:28:04.000Z",
    CategoryId: 3,
    Category: {
      id: 3,
      name: "義大利料理",
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
    },
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
};

export default {
  data() {
    return {
      restaurant: dummyRestaurant.restaurant,
    };
  },
};
</script>