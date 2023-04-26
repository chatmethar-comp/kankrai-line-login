<template>
  <div class="container mx-auto my-12">
    <div class="flex flex-col items-center">
      <h1 class="text-4xl font-semibold text-blue-900 font-Kanit">Kankrai Line Login</h1>
      <button v-show="displayName===''" @click="lineLogin" class="font-bold text-white bg-green-500 text-2xl px-4 py-2">Login with Line</button>
      <img :src="pictureUrl" alt="">
      <h2 class="text-2xl">{{ displayName }}</h2>
      <p>{{ statusMessage }}</p>
      <button v-show="displayName" @click="lineLogout" class="font-bold text-white bg-red-500 text-2xl px-4 py-2">Logout</button>

    </div>
  </div>
</template>

<script setup>
import liff from '@line/liff';
import { ref } from 'vue';

const displayName = ref('');
const pictureUrl = ref('');
const statusMessage = ref('');
const userId = ref('');

liff.init({
    liffId: '1660982627-GnrB0Nkj', // Use own liffId
}).then(()=>{
  if(liff.isLoggedIn()){
    liff.getProfile().then((profile)=>{
      console.log(profile);
      displayName.value = profile.displayName;
      pictureUrl.value = profile.pictureUrl;
      statusMessage.value = profile.statusMessage;
      userId.value = profile.userId;
    })
  }
})

const lineLogin = () => {
  liff.init({
    liffId: '1660982627-GnrB0Nkj', // Use own liffId
  }).then(() => {
      // Redirect to another page after the returned Promise object has been resolved
      // window.location.replace('https://liff.line.me/1660982627-GnrB0Nkj/path');
      console.log(liff.getLanguage());
      console.log(liff.getVersion());
      console.log(liff.isInClient());
      console.log(liff.isLoggedIn());
      console.log(liff.getOS());
      console.log(liff.getLineVersion());
      if (!liff.isLoggedIn()) {
          liff.login();
      } else {
          liff.getProfile().then((profile)=>{
            console.log(profile);
            displayName.value = profile.displayName;
            pictureUrl.value = profile.pictureUrl;
            statusMessage.value = profile.statusMessage;
            userId.value = profile.userId;
          })
      }
  })
}

  const lineLogout = () => {
    liff.logout();
    window.location.reload();
    displayName.value = '';
    pictureUrl.value = '';
    statusMessage.value = '';
    userId.value = '';
  }

</script>

<style lang="scss" scoped>

</style>