<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">User Data</h4>
      </b-row>
      <b-col cols="6">
        <b-form-group id="name" label="Name" label-for="name">
          <b-form-input
            disabled
            id="name"
            type="text"
            placeholder="Name"
            v-model="user.name"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-3">
      <b-col cols="6">
        <b-form-group id="email" label="E-Mail" label-for="email">
          <b-form-input
            disabled
            id="email"
            type="email"
            placeholder="example@cloudappi.com"
            v-model="user.email"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
  </b-form>
</template>

<script>
import axios from "axios";

export default {
  name: "UserDetailsModal",
  props: {
    userId: Number,
  },
  data() {
    return {
      user: {},
    };
  },
  mounted() {
    this.getUserByID();
  },
  methods: {
    getUserByID() {
      axios
        .get(`https://my-user-manager.herokuapp.com/users/${this.userId}`)
        .then((response) => {
          this.user = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
