<template>
  <div class="modal fade" :class="{ show: isShow }">
    <div class="dialog">
      <div ref="modalRef" class="content">
        <div>
          <p>アラートメッセージ</p>
        </div>
        <div>
          <button @click="onClose">キャンセル</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";
import { onClickOutside } from "@vueuse/core";
import { onKeyStroke } from "@vueuse/core";
const emits = defineEmits(["close"]);
const modalRef = ref(null);

const isShow = ref(false);

onMounted(async () => {
  // ふわっとしたトランジションで表示させるように、描画後におこなう。
  await nextTick();
  setTimeout(() => {
    console.log("start open transition");
    isShow.value = true;
  }, 50);
});

const onClose = () => {
  closeModal();
};

const closeModal = () => {
  console.log("start close transition");
  isShow.value = false;
  // ふわっとしたトランジションで非表示するように、トランジションが終わるまで（200ms）emitの発行を待つ。
  setTimeout(() => {
    console.log("close");
    emits("close");
  }, 200);
};

// ダイアログ外を押した時にモーダルを閉じる
onClickOutside(modalRef, () => {
  console.info("click outside");
  onClose();
});

// ESCキー押下時にモーダルを閉じる
onKeyStroke("Escape", (e) => {
  console.info("key stroke Escape");
  e.preventDefault();
  closeModal();
});
</script>

<style scoped lang="css">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  background-color: rgb(0, 0, 0, 0.75);
}

.fade:not(.show) {
  opacity: 0;
}

.fade {
  transition: opacity 0.2s linear;
}

.dialog {
  max-width: 500px;
  margin: 5rem auto;
}

.content {
  position: relative;
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  padding: 2rem;
  justify-content: center;
  background-color: white;
  border-radius: 1rem;
}
</style>

