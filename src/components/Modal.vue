<template>
  <div class="modal">
    <div class="modal-head">
      <h2 class="modal-title"> {{ props.title }} </h2>
      <b class="close-btn" @click="$emit('close')">x</b>
    </div>
    <slot></slot>
    <div class="button-block">
      <button class="confirm-btn" @click="handleConfirm">ok</button>
    </div>
  </div>
</template>


<script setup lang="ts">
const props = defineProps({
  title: String,
  selectedId: Number
});

const emit = defineEmits();

const handleConfirm = () => {
  emit('select', props.selectedId);
  console.log("Selected : ", props.selectedId)
  emit('close');
};

</script>


<style scoped>
.modal {
  border: 1px solid black;
  padding: 15px;
  width: 500px;
}

.modal-head {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}

.close-btn {
  cursor: pointer;
}

.button-block {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
