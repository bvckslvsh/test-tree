<template>
  <div class="wrapper">
    <h1>hello there! No styles due to low budget</h1>
    <button v-if="!isModalOpened" class="openBtn" @click='toggleModal'>Открыть</button>
    <Modal v-if="isModalOpened" :title="'Tree folder structure'" :selectedId="selectedFolder" @select="handleSelect"
      @close="toggleModal">
      <Tree :folders="mockFolders" :selectedId="selectedFolder" @update:selectedId="handleSelect" />
    </Modal>
    <span>debug - selected folder id - {{ selectedFolder }}</span>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Modal from './Modal.vue'
import Tree from './Tree.vue'

const isModalOpened = ref<Boolean>(false);
const selectedFolder = ref<Number | null>(null);

const toggleModal = () => {
  isModalOpened.value = !isModalOpened.value;
}

const updateSelectedId = (id: Number) => {
  selectedFolder.value = id;
}

const mockFolders = [{
  id: 1, name: 'Папка 1', children: [{
    id: 2, name: 'Папка 1.1', children: []
  }, {
    id: 3, name: 'Папка 1.2', children: [{
      id: 4, name: 'Папка 1.2.1', children: []
    }]
  }]
}, { id: 5, name: 'Папка 2', children: [] },];

const handleSelect = (folderId: Number) => {
  selectedFolder.value = folderId;
}

</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 30px;
}

.openBtn {
  width: 150px;
  height: 50px;
}
</style>
