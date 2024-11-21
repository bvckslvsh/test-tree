<template>
  <div class="tree">
    <NodeTree v-for="folder in folders" :key="folder.id" :folder="folder" :selectedId="selectedId"
      @update:selectedId="updateSelectedId" />
  </div>
</template>

<script setup lang="ts">
import NodeTree from './NodeTree.vue';
import { defineProps, defineEmits } from 'vue';
import { IFolder } from '../DTO/types/IFolder.ts';

const props = defineProps({
  folders: Array as () => IFolder[],
  selectedId: Number,
});

const emits = defineEmits(['update:selectedId']);

const updateSelectedId = (folderId: Number) => {
  emits('update:selectedId', folderId);
};
</script>

<style>
.tree {
  padding-left: 10px;
}
</style>

