<template>
  <div class="shows-edit">
    <h1>Edit Show</h1>
    <form v-on:submit.prevent="updateShow(show)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="show.title" />
      Year:
      <input type="text" v-model="show.year" />
      Description:
      <input type="text" v-model="show.description" />
      Creator:
      <input type="text" v-model="show.creator" />
      Seasons:
      <input type="text" v-model="show.seasons" />
      Netowrk:
      <input type="text" v-model="show.netowrk" />
      Favorite:
      <input type="text" v-model="show.favorite" />
      Image:
      <input type="text" v-model="show.image" />
      User ID:
      <input type="text" v-model="show.user_id" />

      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      show: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/shows/" + this.$route.params.id).then((response) => {
      console.log("shows show", response);
      this.show = response.data;
    });
  },
  methods: {
    updateShow: function (show) {
      var editshowParams = show;
      axios
        .patch("/shows/" + show.id, editshowParams)
        .then((response) => {
          console.log("shows update", response);
          this.$router.push("/shows");
        })
        .catch((error) => {
          console.log("shows update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
