<template>
  <div class="container mx-auto my-12">
    <div class="flex flex-col items-center">
      <h2 class="text-4xl font-semibold text-blue-900 uppercase font-Kanit">Kankrai Line Login</h2>
      <button @click="lineLogin" class="font-bold text-white bg-green-500 text-2xl px-4 py-2">Login with Line</button>
    </div>
  </div>
</template>

<script setup>
import liff from '@line/liff';
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
      }
      if (!liff.isLoggedIn() && !liff.isInClient()) {
          window.alert('To get an access token, you need to be logged in. Tap the "login" button below and try again.');
      } else {
          const accessToken = liff.getAccessToken();
          console.log(accessToken);
      }
  });

  
}

</script>

<style lang="scss" scoped>

</style>