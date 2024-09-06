<template>
  <div>
    <h2>회원으로 등록하고 로그인하세요</h2>

    <!-- 버튼들 -->
    <button
      v-for="tab in tabs"
      :key="tab.index"
      :class="['tab-button', { active: currentTab === tab }]"
      @click="currentTab = tab"
    >
      {{ tab }}
    </button>
    <component :is="currentTab" class="tab" />
  </div>
</template>

<script>
import FirstComponent from "@/components/FirstComponent.vue";
import SecondComponent from "@/components/SecondComponent.vue";
// 각 컴포넌트를 정의

export default {
  components: {
    FirstComponent,
    SecondComponent,
  },
  data() {
    return {
      currentTab: "FirstComponent",
      tabs: ["FirstComponent", "SecondComponent"],
    };
  },
};
</script>

<style>
.demo {
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  user-select: none;
  overflow-x: auto;
}

.tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #a1a1a1;
  margin-bottom: -1px;
  margin-right: -1px;
}
.tab-button:hover {
  background: #f0f0f0;
}
.tab-button.active {
  background: #f0f0f0;
}
.tab {
  width: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #ccc;
  padding: 10px;
}
.form {
  width: 60%;
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 10px;
}
</style>
