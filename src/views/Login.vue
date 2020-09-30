<template>
  <form class="" @submit.prevent="login">
    <div class="form-group">
      <label for="username">Username</label>
      <input
        v-model="user.username"
        type="username"
        class="form-control"
        id="username"
        aria-describedby="usernameHelp"
        placeholder="Enter Username"
        required
      />
    </div>
    <div class="form-group">
      <label for="password">Password</label>
      <input
        v-model="user.password"
        type="password"
        class="form-control"
        id="password"
        placeholder="Password"
        required
      />
    </div>
    <button type="submit" class="btn btn-primary">Log In</button>
    <router-link :to="{ name: 'signup' }" class="btn btn-primary ml-3"
      >Sign Up</router-link
    >
  </form>
</template>

<script>
import router from "../router";

export default {
  name: "signup",
  components: {},
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    async login() {
      const requestOptions = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          username: this.user.username,
          password: this.user.password,
        }),
      };
      try {
        const response = await fetch(
          "http://192.168.0.25:4100/users/login",
          requestOptions
        );
        const data = await response.json();
        if (data.user) {
          this.$cookies.set("token", data.accessToken);
          router.push({ path: "/tasks" });
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style></style>
