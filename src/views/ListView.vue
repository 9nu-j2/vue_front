<template>
  <div>
    <div>
      <h1>운영중인 상점</h1>
      <button @click="openModal = true">등록하기</button>
      <div v-if="openModal == true">
        <AddStore />
      </div>
    </div>

    <div>상점 리스트 뿌리기</div>
    <div>
      <div>로그아웃</div>
      <div>동네 소식 나누러가기</div>
    </div>
  </div>
</template>

<script>
import AddStore from "@/components/AddStore.vue";

export default {
  components: {
    AddStore,
  },
  data() {
    return {
      openModal: false,
    };
  },
};
</script>
