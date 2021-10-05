<template>
  <div class="shows-show">
    <h2>{{ show.title }}</h2>
    <img v-bind:src="show.image" v-bind:alt="show.title" />
    <p>Title: {{ show.title }}</p>
    <p>Year: {{ show.year }}</p>
    <p>Description: {{ show.description }}</p>
    <p>Creator: {{ show.creator }}</p>
    <p>Seasons: {{ show.seasons }}</p>
    <p>Network: {{ show.network }}</p>
    <p>Favorite: {{ show.favorite }}</p>
    <p>User: {{ show.user_id }}</p>
    <router-link v-bind:to="`/shows/${show.id}/edit`">Edit Show</router-link>
    |
    <button v-on:click="destroyShow(show)">Destroy show</button>
    |
    <router-link to="/shows">Back to Shows</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      show: {},
    };
  },
  created: function () {
    axios.get("/shows/" + this.$route.params.id).then((response) => {
      console.log("shows show", response);
      this.show = response.data;
    });
  },
  methods: {
    destroyShow: function (show) {
      axios.delete("/shows/" + show.id).then((response) => {
        console.log("destroy show", response);
        this.$router.push("/shows");
      });
    },
  },
};
</script>
