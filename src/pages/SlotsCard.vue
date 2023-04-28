<template>
  <q-dialog class="q-pa-lg">
    <q-card class="my-card q-ma-lg">
      <q-card-section class="bg-teal text-white q-pl-xl q-pr-xl">
        <div class="text-h6">Slot</div>
        <div class="text-subtitle2">{{ slottime }}</div>
        <div align="right">
          *Charges May Apply <br />
          {{ this.singleslotCharge }}<br />
          *Wallet Balance <br />
          {{ this.walletBalance }}
        </div>
      </q-card-section>

      <q-card-actions vertical align="center">
        <div class="q-gutter-sm">
          <q-checkbox
            class="q-ma-lg"
            v-for="item in space"
            :key="item.id"
            v-model="item.partial_booked"
            :disable="item.booked"
            label="Space"
            color="teal"
          />
        </div>
        <q-input
          class="q-ma-lg"
          style="width: 80%"
          filled
          v-model="datedata"
          label="Date"
          :disable="true"
        />
        <q-input
          class="q-ma-lg"
          style="width: 80%"
          filled
          v-model="time"
          label="Time"
          :disable="true"
        />
        <q-btn label="Submit" color="teal" @click="bookslot()" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { data } from "autoprefixer";
import { ref } from "vue";

export default {
  name: "slotsComponent",
  data() {
    return {
      datedata: this.date,
      time: this.slottime,
      singleslotCharge: 20,
      walletBalance: 200,
      space: [],
    };
  },
  props: {
    slottime: String,
    date: String,
  },
  mounted() {
    this.loadSlot();
  },
  methods: {
    bookslot() {
      console.log(this.space);
      const a = this.space.filter(
        (data) => data.booked === false && data.partial_booked === true
      );
      if (a.length > 1) {
        this.$q.notify({
          message: "You can book only one slot at a moment",
          color: "negative",
          icon: "warning",
        });
      } else {
        // const params = {
        //   pk: a.id,
        // };
        this.$api
          .put(`http://localhost:8000/slot/slotspaces/${a[0].id}/`, a[0])
          .then((res) => {
            console.log(res.data);
          })
          .catch((err) => {
            console.log(err);
          });
      }

      // this.walletBalance =
      //   this.walletBalance - this.singleslotCharge * a.length;
    },
    loadSlot() {
      const params = {
        date: this.date,
        slot: this.slottime,
      };
      this.$api
        .get("http://localhost:8000/slot/slotspaces", { params })
        .then((res) => {
          console.log(res.data);
          this.space = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
