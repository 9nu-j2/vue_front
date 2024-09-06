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
      <button type="submit">로그인</button>
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
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        // formData를 Axios를 통해 서버로 전송
        const response = await axios.post(
          "http://localhost:8080/members/login",
          this.formData
        );
        console.log("Response:", response.data);
        if (response.data) {
          localStorage.setItem("ownername", this.formData.ownername);
          this.$router.push("/list");
        } else {
          alert("아이디 또는 비밀번호가 일치하지 않습니다.");
        }
      } catch (error) {
        console.error("Error:", error);
        alert("로그인 중 문제가 발생했습니다.");
      }
    },
  },
};
</script>
