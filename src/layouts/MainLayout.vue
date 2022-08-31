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
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label header class="text-grey-8">
          Essential Links
        </q-item-label>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, getCurrentInstance, ref } from "vue";
import { useRoute } from "vue-router/composables";

export default defineComponent({
  name: "MainLayout",
  setup() {
    const leftDrawerOpen = ref(false);

    // `getCurrentInstance` here into dev code works
    console.log(getCurrentInstance().proxy.$root.$route);

    // `getCurrentInstance` in the guard function returns `null`, resulting in an error
    // https://github.com/vuejs/vue-router/blob/ede092d031bf9144433b600b8cce61143cec3c6c/composables.mjs#L11
    const route = useRoute();
    console.log(route);

    // The same goes for vue-apollo-composable when used
    // https://github.com/vuejs/apollo/blob/6c07a47d33e6a59643a3a4f743e8fa43e435abf4/packages/vue-apollo-composable/src/useApolloClient.ts#L38

    // The following method defined into Vue core correctly return the current instance, so the problem doesn't seem to be there
    // https://github.com/vuejs/vue/blob/ee57d9fd1d51abe245c6c37e6f8f2d45977b929e/src/v3/currentInstance.ts#L12

    return { leftDrawerOpen };
  },
});
</script>
