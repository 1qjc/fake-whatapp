<template>
  <div class="flex w-full px-4 py-3 items-center cursor-pointer">
    <img
      class="rounded-full m-1 w-10"
      src="https://random.imagecdn.app/100/100"
      alt="" />
    <div class="w-full">
      <div class="flex justify-between items-center">
        <div class="text-[15px] text-gray-600">Halu</div>
        <div class="text-[15px] text-gray-600">
          {{ new Date().toLocaleString().split(",")[1] }}
        </div>
      </div>

      <div class="flex items-center">
        <CheckAllIcon :size="18" class="mr-1" />
        <div
          class="text-[15px] w-full text-gray-500 flex items-center justify-between">
          lastChatMessage(chat)...
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import CheckAllIcon from "vue-material-design-icons/CheckAll.vue";
</script>

<style lang="scss" scoped></style>
