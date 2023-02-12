<template>
  <div :class="isActive?'bg-gray-200':''" class="flex w-full px-4 py-3 items-center cursor-pointer">
    <img class="rounded-full m-1 w-10" :src="chat.user.picture || ''" alt="" />
    <div class="w-full">
      <div class="flex justify-between items-center">
        <div class="text-[15px] text-gray-600">
          {{ chat.user.firstName }} {{ chat.user.lastName }}
        </div>
        <div class="text-[15px] text-gray-600">
          {{ lastCreatedAt(chat) }}
        </div>
      </div>

      <div class="flex items-center">
        <CheckAllIcon :fillColor="tickColor(chat)" :size="18" class="mr-1" />
        <div
          class="text-[15px] w-full text-gray-500 flex items-center justify-between">
          {{ lastChatMessage(chat) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { toRefs ,computed} from "vue";
  import CheckAllIcon from "vue-material-design-icons/CheckAll.vue";
  import moment from "moment";
  import { useUserStore } from "../store/user-store";
  import { storeToRefs } from "pinia";

  const props = defineProps({ chat: Object });
  const { chat } = toRefs(props);

  const userStore = useUserStore();
  const { sub, userDataForChat } = storeToRefs(userStore);

  const isActive = computed(() => {
    if (userDataForChat.value.length) {
      if (userDataForChat.value[0].sub1 === chat.value.user.sub) {
        return true;
      }
      if (userDataForChat.value[0].sub2 === chat.value.user.sub) {
        return true;
      }
    }
    return false;
  });

  const tickColor = (chat) => {
    let color = "";
    if (chat.sub1 === sub.value) {
      if (chat.sub1HasViewed) color = "#7DF9FF";
      else color = "#B5B5B5";
    }
    if (chat.sub2 === sub.value) {
      if (chat.sub2HasViewed) color = "#7DF9FF";
      else color = "#B5B5B5";
    }
    return color;
  };
  const lastChatMessage = (chat) => {
    return chat.messages[chat.messages.length - 1].message.substring(0, 20);
  };

  const lastCreatedAt = (chat) => {
    if (chat.messages.length) {
      return moment(chat.messages[chat.messages.length - 1].createdAt).format(
        "MMM D YY HH:MM A"
      );
    }
  };
</script>

<style lang="scss" scoped></style>
