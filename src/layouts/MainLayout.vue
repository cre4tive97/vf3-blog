<script setup lang="ts">
import AuthBtn from 'components/auth/AuthBtn.vue';
</script>
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
