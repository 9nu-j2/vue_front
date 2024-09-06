<template>
  <div>
    <div>
      <h1>운영중인 상점</h1>
      <button @click="openModal = true">등록하기</button>
      <div v-if="openModal == true">
        <AddStore v-model:openModal="openModal" />
      </div>
    </div>

    <div>
      <div v-if="loading" class="loading">Loading...</div>

      <div v-if="error" class="error">{{ error }}</div>

      <div v-if="items" v-for="item in items">
        <div>{{ item.storename }}</div>
        <div>{{ item.storedetail }}</div>
      </div>
    </div>
    <div>
      <div>로그아웃</div>
      <div>동네 소식 나누러가기</div>
    </div>
  </div>
</template>

<script>
import AddStore from "@/components/AddStore.vue";
import axios from "axios";

export default {
  components: {
    AddStore,
  },
  data() {
    return {
      openModal: false,
      items: [],
    };
  },
  methods: {},
  // 차트 구성에 필요한 데이터 획득->컴포넌트가 화면에 보이기 직전->라이프사이클 훅
  mounted() {
    console.log("컴포넌트 mounted call");
    // 1. 스프링부트에 요청 -> 데이터 획득 : 통신
    // 0.5초후에 통신 진행(단발성)
    try {
      setTimeout(async () => {
        const ownername = localStorage.getItem("ownername");
        // 스트링부트에서 크로스도메인 처리 추가해서 개발
        const response = await axios.get(
          `http://localhost:8080/members/store/${ownername}`
        );
        console.log(response.data);
        // 데이터에 통신 결과값 설정
        this.items = response.data;
      }, 1000 * 0.5);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
