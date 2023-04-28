<template>
  <q-page class="q-pa-md">
    <h5>Check Availiblity For Parking Spaces</h5>
    <q-input v-model="date" filled type="date" hint="Date of booking" />
    <q-select
      class="q-mt-md"
      outlined
      v-model="model"
      :options="options"
      :dense="dense"
      :options-dense="denseOpts"
      hint="Timing Slots"
      required
    >
      <template v-slot:prepend>
        <q-icon name="event" />
      </template>
    </q-select>
    <!-- <div class="q-pa-md"> -->
    <q-btn
      push
      class="q-mt-md"
      color="primary"
      icon="check"
      label="Check Availibliity"
      @click="checkAvailiblity()"
    />
  </q-page>
</template>

<script>
import { ref } from "vue";
import useQuasar from "quasar/src/composables/use-quasar.js";
import SlotsCard from "./SlotsCard.vue";
export default {
  data() {
    const $q = useQuasar();
    return {
      model: ref(null),
      options: ["10 to 12", "11 to 2", "2 to 4", "4 to 6", "6 to 8"],
      dense: ref(false),
      denseOpts: ref(false),
      date: ref(null),
    };
  },

  methods: {
    checkAvailiblity() {
      console.log(this.flag);
      this.flag = true;
      console.log(this.model, this.date);
      if (this.model === null || this.date === null) {
        this.$q.notify({
          message: "Field is required",
          color: "red",
          icon: "report_problem",
        });
      } else {
        let available = false;
        const params = {
          date: this.date,
          slot: this.model,
        };
        this.$api
          .get("http://localhost:8000/slot/checkavailability", { params })
          .then((res) => {
            console.log(res.data);
            available = res.data.available;
            if (available === false) {
              this.$q.notify({
                message: "No Slots Available",
                color: "negative",
                icon: "warning",
              });
            } else {
              this.$q.dialog({
                component: SlotsCard,
                componentProps: {
                  slottime: this.model,
                  date: this.date,
                },
              });
            }
          })
          .catch((err) => {
            console.log(err);
          });
      }
    },
  },
};
</script>
