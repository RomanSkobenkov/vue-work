<script setup>
import { DATA_TRANSFER_PAYLOAD, MOVE } from "../constants";

const props = defineProps({
  transferData: {
    type: Object,
    required: true,
  },
});

// Метод onDrag добавляет данные о переносимом объекте в DataTransfer. Более подробно о DataTransfer:
// https://developer.mozilla.org/ru/docs/Web/API/DataTransfer
function onDrag({ dataTransfer }) {
  dataTransfer.effectAllowed = MOVE;
  dataTransfer.dropEffect = MOVE;
  dataTransfer.setData(
    DATA_TRANSFER_PAYLOAD,
    JSON.stringify(props.transferData),
  );
}
</script>

<template>
  <!--  div — элемент, который отслеживает событие dragstart и вызывает метод onDrag. Компонент предотвращает события dragover и dragenter -->
  <div
    :draggable="true"
    @dragstart.self="onDrag"
    @dragover.prevent
    @dragenter.prevent
  >
    <slot />
  </div>
</template>

<style scoped lang="scss"></style>
