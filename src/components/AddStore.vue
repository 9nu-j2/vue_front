<template>
  <div class="tab">
    <Form @submit.prevent="submitForm" class="form">
      <input
        v-model="formData.storename"
        id="storename"
        type="text"
        placeholder="storename"
      />
      <input
        v-model="formData.storedetail"
        id="storedetail"
        type="text"
        placeholder="storedetail"
      />
      <button type="submit">등록하기</button>
    </Form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      // form 데이터 저장
      formData: {
        storename: "",
        storedetail: "",
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        // formData를 Axios를 통해 서버로 전송
        let ownername = localStorage.getItem("ownername");
        const response = await axios.post(
          `http://localhost:8080/members/store/${ownername}/add`,
          this.formData
        );
        alert("가게등록 완료!");
        this.$emit("update:openModal", false);
      } catch (error) {
        console.error("Error:", error);
        alert("가게 등록 중 문제가 발생했습니다.");
      }
    },
  },
};
</script>
