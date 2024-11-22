<template>
  <div class="border border-gray shadow p-4 cursor-pointer mt-2">
    <div class="flex justify-between items-center gap-4" @click.stop.prevent="toggleChildren">
      <div class="flex gap-2 items-center">
        <p>{{ folder.name }}</p>
        <Button @click.stop.prevent="clickOK(folder)">
          ОК
        </Button>
      </div>
      <svg v-if="folder.children.length > 0" width="24" height="24" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M5.29289 7.29289C5.68342 6.90237 6.31658 6.90237 6.7071 7.29289L9.99999 10.5858L13.2929 7.29289C13.6834 6.90237 14.3166 6.90237 14.7071 7.29289C15.0976 7.68342 15.0976 8.31658 14.7071 8.70711L10.7071 12.7071C10.3166 13.0976 9.68341 13.0976 9.29289 12.7071L5.29289 8.70711C4.90237 8.31658 4.90237 7.68342 5.29289 7.29289Z" fill="#6B7280"/>
      </svg>
    </div>
    <div v-if="isOpen" class="flex flex-col gap-4 ml-4">
      <FolderItem v-for="item in folder.children" :key="item.id" :folder="item" 
      @selectFolder="$emit('selectFolder', $event)"/>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Button from '../components/button.vue';
import Folder from '../interfaces/folder';

defineProps<{
  folder: Folder;
}>();

const isOpen = ref(false);

function toggleChildren() {
  isOpen.value = !isOpen.value;
}
const emit = defineEmits<{
  (e: 'selectFolder', value: Folder): void
}>();

const clickOK = (folder: Folder) => {
  emit('selectFolder', folder)
}
</script>
