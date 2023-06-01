<template>
  <!-- 展示用戶列表 -->
  <div v-show="info.users.value.length">
    <el-space wrap :size="20">
      <el-card
        v-for="user in info.users.value"
        class="box-card"
        :key="user.login"
        :body-style="{ padding: '10px' }"
      >
        <el-link :href="user.html_url" target="_blank">
          <img :src="user.avatar_url" class="image"
        /></el-link>
        <p>{{ user.login }}</p>
      </el-card>
    </el-space>
  </div>

  <!-- 展示第一次載入 -->
  <h1 v-show="info.isFirst">歡迎光臨</h1>
  <!-- 展示載入中 -->
  <h1 v-show="info.isLoading">載入中</h1>
  <!-- 展示錯誤訊息 -->
  <h1 v-show="info.errorMsg">{{ info.errorMsg }}</h1>
</template>

<script setup lang="ts">
import { emitter } from "@/mitt/mitter";
import { Ref, onMounted, ref } from "vue";

interface Info {
  isFirst: boolean;
  isLoading: boolean;
  users: Ref<{ login: string; html_url: string; avatar_url: string }[]>;
  errorMsg: string;
}

const info: Info = {
  isFirst: true,
  isLoading: false,
  users: ref([]),
  errorMsg: "",
};

onMounted(() => {
  emitter.on("updateUserList", (dataObj) => {
    info.isFirst = false;
    info.isLoading = dataObj.isLoading;
    info.users.value = dataObj.users;
    info.errorMsg = dataObj.errorMsg;
  });
});
</script>

<style scoped>
.box-card {
  width: 250px;
}

.image {
  width: 100%;
  display: block;
}
</style>
