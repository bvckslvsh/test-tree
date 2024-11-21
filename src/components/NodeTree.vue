<template>
  <div>
    <div :class="['node', { selected: isSelected }]" @click="toggleSelect">
      <span v-if="hasChildren" class="toggle" @click.stop="toggleOpen">
        {{ isOpened ? '-' : '+' }}
      </span>
      {{ folder.name }}
    </div>
    <div v-if="isOpened && hasChildren" class="children">
      <NodeTree v-for="child in folder.children" :key="child.id" :folder="child" :selectedId="selectedId"
        @update:selectedId="updateSelectedId" />
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref, defineProps, defineEmits, computed } from 'vue';
import { IFolder } from '../DTO/types/IFolder.ts';

const props = defineProps({
  folder: Object as () => IFolder,
  selectedId: Number
});

const emits = defineEmits(['update:selectedId'])



const isSelected = computed(() => props.selectedId === props.folder.id);
const isOpened = ref(false);
const hasChildren = computed(() => props.folder.children && props.folder.children.length > 0);

const toggleOpen = () => {
  isOpened.value = !isOpened.value;
};

const toggleSelect = () => {
  if (hasChildren.value) {
    toggleOpen();
  }
  emits('update:selectedId', props.folder.id);
};

const updateSelectedId = (id: Number) => {
  emits('update:selectedId', id);
};


</script>

<style>
.node {
  cursor: pointer;
  padding: 5px;
  border-radius: 4px;
}


.node.selected {
  background-color: lightgray;
}


.children {
  padding-left: 15px
}

.toggle {
  font-weight: bold;
}
</style>
