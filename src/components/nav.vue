<script>
import { RouterLink, RouterView } from "vue-router";
export default {
  methods: {
    login: function () {
      this.$router.push("/login");
    },
    register: function () {
      this.$router.push("/register");
    },
  },
  data: () => ({
    drawer: false,
    items: [
      { title: "Login", icon: "mdi-login", url: "/login" },
      { title: "Register", icon: "mdi-account-box", url: "/register" },
      { title: "CRUD", icon: "mdi-database", url: "/crud" },
    ],
    user: {
      name: "example",
      img: "https://randomuser.me/api/portraits/men/1.jpg",
      mail: "example@example.com",
    },
  }),
};
</script>
<template>
<div class="container-fliud">
    <v-card>
      <v-layout>
        <v-navigation-drawer expand-on-hover rail>
          <v-list>
            <RouterLink to="/" class="nav-link active">
              <v-list-item
                :prepend-avatar="user.img"
                :title="user.name"
                :subtitle="user.mail"
              >
              </v-list-item>
            </RouterLink>
          </v-list>

          <v-divider></v-divider>

          <v-list v-for="item in items" density="compact" nav>
            <RouterLink :to="item.url" class="nav-link active">
              <v-list-item :prepend-icon="item.icon" :title="item.title" link>
              </v-list-item>
            </RouterLink>
          </v-list>
        </v-navigation-drawer>

        <v-main style="height: 250px">
          <v-parallax
            src="https://images.hdqwalls.com/wallpapers/lambo-tron-drifting-5k-yb.jpg"
          >
            <div
              class="d-flex flex-column fill-height justify-center align-center text-white"
            >
              <h1 class="text-h4 font-weight-thin mb-4">Lamborghini</h1>
              <h4 class="subheading">The fastest cars on the market</h4>
            </div>
          </v-parallax>
        </v-main>
      </v-layout>
    </v-card>
    <RouterView />
  </div>
</template>
