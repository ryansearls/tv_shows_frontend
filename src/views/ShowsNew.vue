<template>
  <div class="shows-new">
    <h1>New Show</h1>
    <form v-on:submit.prevent="createShow()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="newShowParams.title" />
      Year:
      <input type="text" v-model="newShowParams.year" />
      Description:
      <input type="text" v-model="newShowParams.description" />
      Creator:
      <input type="text" v-model="newShowParams.creator" />
      Seasons:
      <input type="text" v-model="newShowParams.seasons" />
      Network:
      <input type="text" v-model="newShowParams.network" />
      Favorite:
      <input type="text" v-model="newShowParams.favorite" />
      Image:
      <input type="text" v-model="newShowParams.image" />
      User:
      <input type="text" v-model="newShowParams.user_id" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newShowParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createShow: function () {
      axios
        .post("/shows", this.newShowParams)
        .then((response) => {
          console.log("shows create", response);
          this.$router.push("/shows");
        })
        .catch((error) => {
          console.log("shows create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
