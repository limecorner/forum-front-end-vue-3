<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <div v-for="user in users" :key="user.id" class="col-3">
        <a href="#">
          <img
            src="http://via.placeholder.com/300x300?text=No+Image"
            width="140px"
            height="140px"
          />
        </a>
        <h2>{{ user.name }}</h2>
        <span class="badge badge-secondary"
          >追蹤人數：{{ user.FollowerCount }}</span
        >
        <p class="mt-3">
          <button
            v-if="user.isFollowed"
            @click.stop.prevent="onCancelFollow(user)"
            type="button"
            class="btn btn-danger"
          >
            取消追蹤
          </button>
          <button
            @click.stop.prevent="onFollow(user)"
            v-else
            type="button"
            class="btn btn-primary"
          >
            追蹤
          </button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
const dummyUsers = {
  users: [
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$dEj2FuoeieIlkN.GJfoC9O.SwoaY99MfXet4z8vB5wAf12Vwa5NjS",
      isAdmin: true,
      image: null,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$bX6prwanTs8SK6l/74g3UOWAbGURSxcrmvZlCjsFKBfOtz.P6nhba",
      isAdmin: false,
      image: null,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$yRfxRHfliQKntt5GnMdxb.OCB38jf3IFjnnP6Yj180JPqmqD2.URC",
      isAdmin: false,
      image: null,
      createdAt: "2022-03-11T06:14:36.000Z",
      updatedAt: "2022-03-11T06:14:36.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
  ],
};

export default {
  components: {
    NavTabs,
  },
  data() {
    return {
      users: [],
    };
  },
  created() {
    this.fetchUser();
  },
  methods: {
    fetchUser() {
      this.users = dummyUsers.users;
    },
    onFollow(user) {
      this.users = this.users.map((_user) => {
        if (_user.id === user.id) {
          return {
            ..._user,
            isFollowed: true,
          };
        } else {
          return {
            ..._user,
          };
        }
      });
    },
    onCancelFollow(user) {
      this.users = this.users.map((_user) => {
        if (_user.id === user.id) {
          return {
            ..._user,
            isFollowed: false,
          };
        } else {
          return {
            ..._user,
          };
        }
      });
    },
  },
};
</script>