<template>
  <q-btn v-if="firebaseUser" round color="info">
    <q-avatar size="32px">
      <img :src="firebaseUser.photoURL || ''" />
      <q-menu>
        <q-card>
          <q-list>
            <q-item>
              <q-item-section avatar>
                <q-icon name="mdi-account" />
              </q-item-section>
              <q-item-section>
                <q-item-label>이름</q-item-label>
                <q-item-label caption>{{
                  firebaseUser.displayName
                }}</q-item-label>
              </q-item-section>
            </q-item>
            <q-item>
              <q-item-section avatar>
                <q-icon name="mdi-email" />
              </q-item-section>
              <q-item-section>
                <q-item-label>이메일</q-item-label>
                <q-item-label caption>{{ firebaseUser.email }}</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
          <q-card-actions vertical align="right">
            <q-btn
              icon="mdi-logout"
              flat
              label="로그아웃"
              color="primary"
              @click="signOut(auth)"
            />
          </q-card-actions>
        </q-card>
      </q-menu>
    </q-avatar>
  </q-btn>
  <q-btn v-else @click="signInWithPopup(auth, provider)" round color="info">
    <q-avatar icon="mdi-login" size="32px"> </q-avatar>
  </q-btn>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';
import { initializeApp } from 'firebase/app';
import firebaseConfig from '../../../firebaseConfig';
import {
  getAuth,
  connectAuthEmulator,
  GoogleAuthProvider,
  signInWithPopup,
  onAuthStateChanged,
  User,
  signOut,
} from 'firebase/auth';

export default defineComponent({
  name: 'AuthBtn',

  setup() {
    initializeApp(firebaseConfig);
    const auth = getAuth();
    connectAuthEmulator(auth, 'http://localhost:9099');
    auth.useDeviceLanguage();
    const provider = new GoogleAuthProvider();
    const firebaseUser = ref<User | null>(null);
    onAuthStateChanged(auth, (user) => {
      console.log(user);
      firebaseUser.value = user;
    });

    return {
      provider,
      signInWithPopup,
      auth,
      onAuthStateChanged,
      firebaseUser,
      signOut,
    };
  },
});
</script>
