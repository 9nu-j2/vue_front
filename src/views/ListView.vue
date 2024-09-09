<template>
  <div>
    <div>
      <h1>{{ ownername }}이 운영중인 상점</h1>
      <button @click="openModal = true">등록하기</button>
      <div v-if="openModal == true">
        <AddStore v-model:openModal="openModal" />
      </div>
    </div>

    <div>
      <div v-if="loading" class="loading">Loading...</div>

      <div v-if="error" class="error">{{ error }}</div>

      <div v-if="items" v-for="item in items">
        <h3>{{ item.storename }}</h3>
        <p>{{ item.storedetail }}</p>
      </div>
    </div>
    <div>
      <div>로그아웃</div>
      <button @click="submitForm()">동네 소식 나누러 가기</button>
    </div>
  </div>
</template>

<script>
import AddStore from "@/components/AddStore.vue";
import axios from "axios";

const ownername = localStorage.getItem("ownername");
const location = localStorage.getItem("location");

export default {
  components: {
    AddStore,
  },
  data() {
    return {
      openModal: false,
      items: [],
      ownername,
      location,
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await axios.post(`http://localhost:8081/chat`);
        if (response.data) {
          console.log(response.data);
          this.$router.push("/chat");
        }
      } catch (error) {
        console.error("Error:", error);
        alert("채팅 접속 중 문제가 발생했습니다.");
      }
    },
  },
  // 차트 구성에 필요한 데이터 획득->컴포넌트가 화면에 보이기 직전->라이프사이클 훅
  mounted() {
    console.log("컴포넌트 mounted call");
    // 1. 스프링부트에 요청 -> 데이터 획득 : 통신
    // 0.5초후에 통신 진행(단발성)
    try {
      setTimeout(async () => {
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
