<template>
  <div class="fixed top-0 bg-[#00000046] left-0 w-full h-full z-10 flex items-center justify-center">
    <div class="bg-white rounded-md p-6 w-1/2">
      <div class="flex items-center justify-between gap-4">
        <h2 class="text-lg font-medium">
          {{ title }}
        </h2>
        <Button @click="closeModal">
          Закрыть
        </Button>
      </div>
      <div class="flex flex-col gap-2 mt-4">
        <FolderItem v-for="folder in folders" :key="folder.id" :folder="folder"
        class="border border-gray rounded p-4 shadow cursor-pointer"
        @selectFolder="selectFolder">
        </FolderItem>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import Button from '../components/button.vue'
import Folder from '../interfaces/folder';
import FolderItem from '../components/FolderItem.vue';
  defineOptions({
    name: 'ModalComponent'
  })
  defineProps<{
    title: string,
    folders: Folder[]
  }>()
  const emit = defineEmits<{
    (e: 'close'): void,
    (e: 'select', value: Folder): void
  }>();
  const closeModal = () => {
    emit('close')
  }

  const selectFolder = (folder: Folder) =>  {
    emit('select', folder)
  }
</script>