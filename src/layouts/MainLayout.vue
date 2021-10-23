<template>
  <q-layout view="hhh lpr fff" :container="false">
    <q-header>
      <q-toolbar>
        <q-toolbar-title>Blog</q-toolbar-title>
        <AuthBtn />
      </q-toolbar>
    </q-header>
  </q-layout>
  <q-page-container>
    <router-view />
  </q-page-container>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import AuthBtn from 'components/auth/AuthBtn.vue';

export default defineComponent({
  name: 'MainLayout',
  components: {
    AuthBtn,
  },

  setup() {
    //
  },
});
</script>
