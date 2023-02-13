<template>
  <div class="w-full">
    <div class="max-w-xl mx-auto">
      <div class="mt-10 flex items-center w-full">
        <img width="40" src="/vite.svg" alt="" />
        <div class="font-semibold text-gray-600 ml-6">Haloop Login</div>
      </div>

      <div class="px-20 py-36 m-6 mt-20 rounded-lg border-2 border-black">
        <div class="text-center text-4xl text-gray-700 font-light pb-10">
          Haloop
        </div>
        <div class="w-full flex justify-center p-3 rounded-md">
          <GoogleLogin class="" :callback="callback" />
        </div>
        <div class="w-full flex justify-center p-3 rounded-md">
          <button class="border-gray-300 text-sm border-[1px] rounded-md px-12 py-2 hover:bg-blue-100 bg" @click="HaluLogin()"><label for="">Sign in as Halu</label></button>  
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import {useUserStore} from "@/store/user-store";
  import { useRouter } from "vue-router";
  const router = useRouter();
  const userStore = useUserStore();
  const callback = async (res) => {
    await userStore.getUserDetailsFromGoogle(res);
    setTimeout(() => {
      router.push("/");
    }, 200);
  };

  const HaluLogin = async (res) => {
    await userStore.getUserDetailsFromGoogle({credential:"halu"});
    setTimeout(() => {
      router.push("/");
    }, 200);
  };
</script>

<style lang="scss" scoped></style>
