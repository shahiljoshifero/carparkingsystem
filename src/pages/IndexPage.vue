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
    >
      <template v-slot:prepend>
        <q-icon name="event" />
      </template>
    </q-select>
    <q-btn
      class="q-mt-md"
      color="primary"
      icon="check"
      icon-right="send"
      label="Check Availibliity"
    />
  </q-page>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    // console.log(ref);
    return {
      model: ref(null),
      options: ["10 to 12", "11 to 2", "2 to 4", "4 to 6", "6 to 8"],
      dense: ref(false),
      denseOpts: ref(false),
      date: ref(""),
    };
  },
};
</script>
