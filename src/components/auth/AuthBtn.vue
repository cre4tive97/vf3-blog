<template>
  <q-btn @click="signInWithPopup(auth, provider)" round color="info">
    <q-avatar icon="mdi-login" size="24"> </q-avatar>
  </q-btn>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import { initializeApp } from 'firebase/app';
import firebaseConfig from '../../../firebaseConfig';
import {
  getAuth,
  connectAuthEmulator,
  GoogleAuthProvider,
  signInWithPopup,
} from 'firebase/auth';

export default defineComponent({
  name: 'AuthBtn',

  setup() {
    initializeApp(firebaseConfig);
    const auth = getAuth();
    connectAuthEmulator(auth, 'http://localhost:9099');
    auth.useDeviceLanguage();
    const provider = new GoogleAuthProvider();

    return {
      provider,
      signInWithPopup,
      auth,
    };
  },
});
</script>
