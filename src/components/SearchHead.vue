<template>
  <div class="box-card">
    <h1>搜尋 Github 使用者</h1>
    <div class="card-header">
      <input type="text" placeholder="請輸入名稱..." v-model="keyWord" />
      <el-button type="primary" text @click="searchUsers">搜尋</el-button>
    </div>
  </div>
</template>

<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";
import { emitter } from "@/mitt/mitter";

const keyWord = ref("");
const searchUsers = () => {
  // 請求前更新list數據，狀態為isLoading
  emitter.emit("updateUserList", {
    isFirst: false,
    isLoading: true,
    errorMsg: "",
    users: [],
  });
  axios.get(`https://api.github.com/search/users?q=${keyWord.value}`).then(
    (response) => {
      // 請求成功後更新list數據，狀態為顯示users
      emitter.emit("updateUserList", {
        isLoading: false,
        errorMsg: "",
        users: response.data.items,
      });
    },
    (error) => {
      // 請求失敗後更新list數據，狀態為顯示errorMsg
      emitter.emit("updateUserList", {
        isLoading: false,
        errorMsg: error.message,
        users: [],
      });
    }
  );
};
</script>

<style scoped>
.card-header {
  display: flex;
  align-items: center;
  justify-content: center;
}

.box-card {
  width: 100%;
  margin-bottom: 20px;
  position: relative;
  align-items: center;
  justify-content: center;
}

.card-header input {
  height: 22px;
  width: 500px;
}

.card-header button {
  margin-left: 5px;
  border: 1px solid #eee;
}
</style>
