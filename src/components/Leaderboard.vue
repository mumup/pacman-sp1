<template>
  <div class="leaderboard-container">
    <div class="leaderboard-header">
      <h2 class="leaderboard-title"></h2>
      <button class="refresh-button" @click="refreshData" :disabled="loading">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="refresh-icon"
          :class="{ rotating: loading }"
        >
          <path
            d="M21.5 2v6h-6M2.5 22v-6h6M2 11.5a10 10 0 0 1 18.8-4.3M22 12.5a10 10 0 0 1-18.8 4.2"
          />
        </svg>
      </button>
    </div>

    <div class="leaderboard-content">
      <div v-if="loading" class="loading-container">
        <div class="loading-spinner"></div>
        <p>Loading...</p>
      </div>

      <div v-else-if="error" class="error-container">
        <p>{{ error }}</p>
        <button class="retry-button" @click="refreshData">Retry</button>
      </div>

      <div v-else-if="leaderboardData.length === 0" class="empty-container">
        <p>Empty</p>
      </div>

      <table v-else class="leaderboard-table">
        <thead>
          <tr>
            <th class="rank-column">rank</th>
            <th class="player-column">player</th>
            <th class="score-column">score</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(item, index) in leaderboardData"
            :key="index"
            :class="{ 'current-user': item.isCurrentUser }"
          >
            <td class="rank-column">
              <div class="rank-badge" :class="getRankClass(index)">
                {{ index + 1 }}
              </div>
            </td>
            <td class="player-column">
              <div class="player-info">
                <div
                  class="player-avatar"
                  :style="{ backgroundColor: getAvatarColor(item.playerName) }"
                >
                  {{ getInitials(item.playerName) }}
                </div>
                <span class="player-name">{{ item.playerName }}</span>
              </div>
            </td>
            <td class="score-column">{{ item.score }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { client } from '@/utils/http'

// 定义响应式状态
const leaderboardData = ref([]);
const loading = ref(false);
const error = ref(null);

// 模拟数据获取函数
async function fetchLeaderboardData() {
  loading.value = true;
  error.value = null;

  try {
    // 这里可以替换为实际的API调用
    const response = await client.get(
      "scores/leaderboard"
    );

    console.log(response, 'responseresponse')

    return response.data.data;
  } catch (err) {
    console.error("获取排行榜数据失败:", err);
    throw new Error("Failed to obtain the ranking list data.");
  } finally {
    loading.value = false;
  }
}

// 刷新数据
async function refreshData() {
  if (loading.value) return;

  try {
    leaderboardData.value = await fetchLeaderboardData();
    error.value = null;
  } catch (err) {
    error.value = err.message;
  }
}

// 获取排名样式
function getRankClass(index) {
  if (index === 0) return "rank-first";
  if (index === 1) return "rank-second";
  if (index === 2) return "rank-third";
  return "";
}

// 获取头像颜色
function getAvatarColor(name) {
  // 简单的字符串哈希算法生成颜色
  let hash = 0;
  for (let i = 0; i < name.length; i++) {
    hash = name.charCodeAt(i) + ((hash << 5) - hash);
  }

  const hue = Math.abs(hash % 360);
  return `hsl(${hue}, 70%, 60%)`;
}

// 获取名字首字母
function getInitials(name) {
  return name.charAt(0).toUpperCase();
}

// 组件挂载时加载数据
onMounted(() => {
  refreshData();
});
</script>

<style scoped>
.leaderboard-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

.leaderboard-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  border-bottom: 1px solid #e0e0e0;
}

.leaderboard-title {
  margin: 0;
  font-size: 16px;
  font-weight: 600;
  color: #333;
}

.refresh-button {
  background: transparent;
  border: none;
  width: 28px;
  height: 28px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #666;
  transition: all 0.2s ease;
}

.refresh-button:hover {
  background-color: rgba(0, 0, 0, 0.05);
  color: #333;
}

.refresh-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.refresh-icon {
  transition: transform 0.5s ease;
}

.refresh-icon.rotating {
  animation: rotate 1s linear infinite;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.leaderboard-content {
  flex: 1;
  overflow-y: auto;
  padding: 0;
}

.loading-container,
.error-container,
.empty-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  color: #666;
  text-align: center;
  padding: 20px;
}

.loading-spinner {
  width: 30px;
  height: 30px;
  border: 3px solid rgba(0, 0, 0, 0.1);
  border-radius: 50%;
  border-top-color: #fe11c5;
  animation: spin 1s ease-in-out infinite;
  margin-bottom: 10px;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.retry-button {
  margin-top: 10px;
  padding: 6px 12px;
  background-color: #f0f0f0;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.retry-button:hover {
  background-color: #e0e0e0;
}

.leaderboard-table {
  width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
}

.leaderboard-table th {
  padding: 12px 16px;
  text-align: left;
  font-weight: 500;
  color: #666;
  border-bottom: 1px solid #eaeaea;
  font-size: 12px;
  text-transform: uppercase;
}

.leaderboard-table td {
  padding: 12px 16px;
  border-bottom: 1px solid #f0f0f0;
}

.leaderboard-table tr:last-child td {
  border-bottom: none;
}

.leaderboard-table tr:hover {
  background-color: rgba(0, 0, 0, 0.02);
}

.rank-column {
  width: 60px;
}

.score-column {
  width: 80px;
  text-align: right;
  font-weight: 600;
}

.rank-badge {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background-color: #f0f0f0;
  font-weight: 600;
  font-size: 14px;
  color: #666;
}

.rank-first {
  background-color: #ffd700;
  color: #5d4037;
}

.rank-second {
  background-color: #c0c0c0;
  color: #5d4037;
}

.rank-third {
  background-color: #cd7f32;
  color: #5d4037;
}

.player-info {
  display: flex;
  align-items: center;
}

.player-avatar {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 10px;
  color: white;
  font-weight: 600;
  font-size: 14px;
}

.player-name {
  font-weight: 500;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.current-user {
  background-color: rgba(254, 17, 197, 0.05);
}

.current-user .player-name {
  color: #fe11c5;
  font-weight: 600;
}
</style>
