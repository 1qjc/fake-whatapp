<template>
  <router-view />
</template>

<script setup>
  import {useUserStore} from "@/store/user-store";
  import { onMounted } from "vue";
  import { useRouter } from "vue-router";
  const router = useRouter();
  const userStore = useUserStore();

  onMounted(() => {
    if (!userStore.sub) router.push("/login");
  });
</script>
