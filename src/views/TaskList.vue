<template>
  <ul class="list-group">
    <li v-for="task in tasks" :key="task.id" class="list-group-item">
      {{ task.day }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "tasklist",
  data() {
    return {
      msg: "hello",
      accessToken: this.$cookies.get("token"),
      tasks: null,
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      const requestOptions = {
        method: "GET",
        headers: {
          authorization: "Bearer " + this.accessToken,
        },
      };
      const response = await fetch(
        "http://192.168.0.25:4100/tasks/" + this.$cookies.get("user"),
        requestOptions
      );
      const data = await response.json();

      if (data.err) {
        console.log(data.err);
      } else {
        this.tasks = data;
        console.log(data);
      }
    },
  },
};
</script>

<style></style>
