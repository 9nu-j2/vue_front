<template>
  <div class="tab">
    <Form @submit.prevent="submitForm" class="form">
      <input
        v-model="formData.ownername"
        id="ownername"
        type="text"
        placeholder="ownername"
      />
      <input
        v-model="formData.password"
        id="password"
        type="text"
        placeholder="password"
      />
      <input
        v-model="formData.location"
        id="location"
        type="text"
        placeholder="location"
      />
      <button type="submit">가입하기</button>
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
        ownername: "",
        password: "",
        location: "",
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        // formData를 Axios를 통해 서버로 전송
        const response = await axios.post(
          "http://localhost:8080/members",
          this.formData
        );
        alert("회원가입이 완료되었습니다!");
        if (response.data.ownername === this.formData.ownername) {
          this.$router.push("/list");
        }
      } catch (error) {
        console.error("Error:", error);
        alert("회원가입 중 문제가 발생했습니다.");
      }
    },
  },
};
</script>
