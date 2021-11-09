<template>
  <div>
    <b-row class="mt-3">
      <b-card>
        <b-row align-h="between">
          <b-col>
            <h3>{{ tableHeader }}</h3>
          </b-col>
        </b-row>
        <b-row class="mt-3">
          <b-table
            striped
            hover
            :items="items"
            :fields="fields"
            class="text-center"
          >
            <template #cell(actions)="data">
              <b-row>
                <b-col>
                  <b-icon-search
                    class="action-item"
                    variant="primary"
                    @click="getRowData(data.item.id)"
                  ></b-icon-search>
                </b-col>
              </b-row>
            </template>
          </b-table>
        </b-row>
      </b-card>
    </b-row>

    <!-- Modal for user details -->
    <b-modal ref="user-details-modal" size="xl" hide-footer title="Details">
      <user-details-form :userId="userId"></user-details-form>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
import UserDetailsForm from "@/components/UserDetailsForm.vue";

export default {
  components: {
    UserDetailsForm,
  },
  data() {
    return {
      // Note 'isActive' is left out and will not appear in the rendered table

      fields: [
        {
          key: "name",
          label: "User Name",
          sortable: false,
        },
        {
          key: "email",
          label: "User E-Mail",
          sortable: false,
        },
        {
          key: "actions",
          label: "Details",
          sortable: false,
        },
      ],
      items: [],
      userId: 0,
      tableHeader: "",
    };
  },
  mounted() {
    this.getUserData();
  },
  methods: {
    getUserData() {
      axios
        .get("https://my-user-manager.herokuapp.com/users")
        .then((response) => {
          this.tableHeader = "Users";
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getRowData(id) {
      this.$refs["user-details-modal"].show();
      this.userId = id;
    },
  },
};
</script>

<style>
.action-item:hover {
  cursor: pointer;
}
</style>
