<template>
  <div class="flex">
    <!-- header -->
    <div id="Header" class="fixed w-[420px] z-10">
      <div
        class="bg-[#F0F0F0] w-full flex justify-between items-center px-3 py-2">
        <img
          class="rounded-full ml-1 w-10"
          :src="userStore.picture || userStore.lastName" />
        {{ userStore.firstName }}
        <div class="flex items-center justify-center">
          <AccountGroupIcon fillColor="#515151" class="mr-6" />
          <DotsVerticalIcon
            @click="logout"
            fillColor="#515151"
            class="cursor-pointer" />
        </div>
      </div>
      <div id="Search" class="bg-white w-full px-2 border-b shadow-sm">
        <div
          class="px-1 m-2 bg-[#F0F0F0] flex items-center justify-center rounded-md">
          <MagnifyIcon fillColor="#515151" :size="18" class="mr-6" />
          <input
            @click="showFindFriends = !showFindFriends"
            class="ml-5 apperance-none w-full bg-[#F0F0F0] py-1.5 px-2.5 text-gray-700 leading-tight focus:outline-none focus:shadow-outline placeholder:text-sm placeholder:text-gray-500"
            type="text"
            autocomplete="off"
            placeholder="Start a new chat" />
        </div>
      </div>
    </div>

    <!-- find friends -->
    <div v-if="showFindFriends">
      <FindFriendsView class="pt-28" />
    </div>
    <!-- chat -->
    <div v-else>
      <ChatView class="mt-[100px]" />
    </div>

    <!-- message -->
    <div v-if="userDataForChat.length">
      <MessageView />
    </div>
    <div v-else>
      <div
        class="ml-[420px] fixed w-[calc(100vw-420px)] h-[100vh] bg-gray-100 text-center">
        <div class="grid h-screen place-items-center">
          <div>
            <div class="w-full flex items-center justify-center">
              <img
                width="375"
                src="https://random.imagecdn.app/400/200"
                alt="img" />
            </div>
            <div class="text-gray-500 font-light mt-10">Haloop</div>
            <div class="text-[14px] text-gray-600 mt-2">
              <div>
                Send and receive messages with keeping your phone online.
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import ChatView from "./ChatView.vue";
  import MessageView from "./MessageView.vue";
  import FindFriendsView from "./FindFriendsView.vue";

  import AccountGroupIcon from "vue-material-design-icons/AccountGroup.vue";
  import DotsVerticalIcon from "vue-material-design-icons/DotsVertical.vue";
  import MagnifyIcon from "vue-material-design-icons/Magnify.vue";

  import { onMounted, ref } from "vue";
  import { useUserStore } from "@/store/user-store";
  import { useRouter } from "vue-router";
  import { storeToRefs } from "pinia";

  const router = useRouter();
  const userStore = useUserStore();

  const { showFindFriends,userDataForChat } = storeToRefs(userStore);

  onMounted(async () => {
    try {
      await userStore.getAllUsers();
      await userStore.getAllChatsByUser();
    } catch (error) {
      console.log(error);
    }
  });

  const logout = () => {
    let res = confirm("are you sure you want to logout?");
    if (res) {
      userStore.logout();
      router.push("/login");
    }
  };
</script>

<style lang="scss"></style>
