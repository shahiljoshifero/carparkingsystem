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
    <div class="q-pa-md">
      <q-btn
        push
        class="q-mt-md"
        color="primary"
        icon="check"
        icon-right="send"
        label="Check Availibliity"
        @click="checkAvailiblity()"
      />
      <q-popup-proxy>
        <q-banner color="">
          <template v-slot:avatar>
            <q-icon name="check" color="primary" />
          </template>
          {{ model }} Slot Is Available for Date {{ date }}
        </q-banner>
      </q-popup-proxy>
    </div>

    <div class="q-pa-md">
      <div class="row q-gutter-sm">
        <q-btn
          no-caps
          unelevated
          color="positive"
          @click="triggerPositive"
          label="Trigger 'positive'"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import { ref } from "vue";
import useQuasar from "quasar/src/composables/use-quasar.js";
export default {
  setup() {
    const $q = useQuasar();
    return {
      triggerPositive() {
        $q.notify({
          type: "positive",
          message: 'This is a "positive" type notification.',
        });
      },

      model: ref(null),
      options: ["10 to 12", "11 to 2", "2 to 4", "4 to 6", "6 to 8"],
      dense: ref(false),
      denseOpts: ref(false),
      date: ref(""),
    };
  },

  methods: {
    checkAvailiblity() {
      console.log(this.model, this.date);
    },
  },
};
</script>
