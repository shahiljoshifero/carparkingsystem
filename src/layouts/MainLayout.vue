<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>

      <q-toolbar-title class="absolute-center">
        Car Parking System
      </q-toolbar-title>
      <!-- <div class="q-px-lg q-mb-md">
        <div class="text-h3">CarParkingSystem</div>
      </div> -->
      <!-- <q-img src="~assets/mountain.jpg" class="header-image absolute-top" /> -->
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="200"
      :breakpoint="600"
      class="q-mt-md"
    >
      <q-scroll-area
        style="
          height: calc(100% - 150px);
          margin-top: 150px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item clickable exact v-ripple to="/">
            <q-item-section avatar>
              <q-icon name="home" />
            </q-item-section>

            <q-item-section> Home </q-item-section>
          </q-item>
          <q-item clickable exact v-ripple to="/slots">
            <q-item-section avatar>
              <q-icon name="today" />
            </q-item-section>

            <q-item-section> Slots </q-item-section>
          </q-item>
          <q-item clickable exact v-ripple to="/customer">
            <q-item-section avatar>
              <q-icon name="man" />
            </q-item-section>

            <q-item-section> Customer </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="~assets/mountain.jpg"
        style="height: 164px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
          </q-avatar>
          <div class="text-weight-bold">Shahil Joshi</div>
          <div>@shahiljoshi9827</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <KeepAlive>
        <router-view />
      </KeepAlive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  components: {},

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.9;
}
</style>
