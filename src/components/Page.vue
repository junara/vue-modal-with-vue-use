<template>
  <div>
    <div>
      <button @click="onOpen">開く</button>
    </div>
    <Modal v-if="isShow" @close="onClose" />
  </div>
</template>
<script setup>
import { ref } from "vue";
import Modal from "./Modal.vue";

const isShow = ref(false);

const onOpen = () => {
  isShow.value = true;
};

const onClose = () => {
  isShow.value = false;
};
</script>
