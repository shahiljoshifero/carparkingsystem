<template>
  <q-page class="q-pa-lg">
    <!-- <h5 class="q-mt-none">Custo</h5> -->
    <div class="row">
      <q-table
        title="Customers"
        :rows="posts"
        :columns="columns"
        row_key="id"
        class="col"
      >
        <template v-slot:body-cell-actions="props">
          <q-td :props="props">
            <q-btn icon="account_balance_wallet" @click="bar2 = true">
              <q-tooltip class="bg-primary">Make Topup</q-tooltip>
            </q-btn>
            <q-btn icon="visibility" @click="bar1 = true">
              <q-tooltip class="bg-primary">View Ledger</q-tooltip>
            </q-btn>
          </q-td>
        </template>
      </q-table>
      <q-dialog
        v-model="bar2"
        persistent
        transition-show="flip-down"
        transition-hide="flip-up"
      >
        <q-card class="bg-primary text-white">
          <q-bar>
            <div>9:34</div>

            <q-space />

            <q-btn dense flat icon="close" v-close-popup>
              <q-tooltip class="bg-white text-primary">Close</q-tooltip>
            </q-btn>
          </q-bar>

          <q-card-section>
            <div class="text-h6">Add Money To Your Wallet</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <q-input
              outlined
              bottom-slots
              v-model="text"
              label="amount"
              :dense="dense"
            >
              <template v-slot:hint> Add Amount </template>

              <template v-slot:after>
                <q-btn round dense flat icon="send" />
              </template>
            </q-input>
          </q-card-section>
        </q-card>
      </q-dialog>
      <q-dialog
        v-model="bar1"
        transition-show="rotate"
        transition-hide="rotate"
      >
        <q-card>
          <q-card-section>
            <div class="text-h6">Terms of Agreement</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <template>
              <div class="q-pa-md row justify-center">
                <div style="width: 100%; max-width: 400px">
                  <q-chat-message
                    name="me"
                    :text="['hey, how are you?']"
                    sent
                  />
                  <q-chat-message
                    name="Jane"
                    :text="['doing fine, how r you?']"
                  />
                </div>
              </div>
            </template>
          </q-card-section>
        </q-card>
      </q-dialog>
    </div>
  </q-page>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    return {
      bar2: ref(false),
      bar1: ref(false),
    };
  },

  data() {
    return {
      columns: [
        {
          name: "id",
          label: "Post",
          field: "id",
          align: "left",
          sortable: true,
        },
        {
          name: "name",
          label: "Name",
          field: "name",
          align: "left",
          sortable: true,
        },
        {
          name: "username",
          label: "UserName",
          field: "username",
          align: "left",
          sortable: true,
        },
        {
          name: "phone",
          label: "Phone",
          field: "phone",
          align: "left",
          sortable: true,
        },
        { name: "actions", label: "Action" },
      ],
      posts: [],
    };
  },
  mounted() {
    // this.setup();
    this.getPosts();
  },
  methods: {
    getPosts() {
      this.$api
        .get("/users")
        .then((res) => {
          // console.log(res);
          this.posts = res.data;
          console.log(res.data);
          // print(res);
        })
        .catch((err) => {
          // print(err);
          console.log(err);
        });
    },
  },
};
</script>
