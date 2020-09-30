<template>
  <form class="" @submit.prevent="signup">
    <div class="form-group">
      <label for="email">Email address</label>
      <input
        v-model="user.email"
        type="email"
        class="form-control"
        id="email"
        aria-describedby="emailHelp"
        required
      />
      <small id="emailHelp" class="form-text text-muted"
        >We'll never share your email with anyone else.</small
      >
    </div>
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
    <div class="form-row">
      <div class="form-group col-md-6">
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
      <div class="form-group col-md-6">
        <label for="confirmPassword">Confirm Password</label>
        <input
          v-model="user.confirmPassword"
          type="password"
          class="form-control"
          id="confirmPassword"
          placeholder="Confirm Password"
          required
        />
      </div>
    </div>
    <button type="submit" class="btn btn-primary">Sign Up</button>
    <router-link :to="{ name: 'login' }" class="btn btn-primary ml-3"
      >Log In</router-link
    >
  </form>
</template>

<script>
export default {
  created() {
    if (this.$cookies.get("token")) {
      console.log(this.$cookies.get("token"));
    }
  },
  name: "signup",
  components: {},
  data() {
    return {
      user: {
        username: "",
        email: "",
        password: "",
        confirmPassword: "",
      },
    };
  },
  methods: {
    async signup() {
      console.log("submitted");
      if (this.user.password !== this.user.confirmPassword) {
        console.log("passwords do not match");
      } else {
        const requestOptions = {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            username: this.user.username,
            password: this.user.password,
            email: this.user.email,
          }),
        };
        await fetch("http://192.168.0.25:4100/users/create", requestOptions);
      }
    },
  },
};
</script>

<style></style>
