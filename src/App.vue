<script setup lang="ts">
import Button from './components/button.vue'
import Modal from './components/modal.vue';
import { ref } from 'vue';
import Folder from './interfaces/folder';

let showModal = ref(false)

const mockFolders: Folder[] =  [
  { id: 1, name: 'Папка 1', children: [
    { id: 2, name: 'Папка 1.1', children: [] },
    { id: 3, name: 'Папка 1.2', children: [
      { id: 4, name: 'Папка 1.2.1', children: [] }
    ]}
  ]},
  { id: 5, name: 'Папка 2', children: [] },
];

const activeFolder = ref<Folder>({
  id: 0,
  name: '',
  children: []
})

const closeModal = () => {
  showModal.value = false
}
const openModal = () => {
  showModal.value = true
}
const select = (folder: Folder) => {
  activeFolder.value = folder
  closeModal()
}

</script>

<template>
  <div class="relative p-4">
    <div class="flex items-center gap-4">
      <Button @click="openModal">
        Открыть
      </Button>
      <p v-if="activeFolder.name">
        Выбранный пакет: {{ activeFolder.name }}
      </p>
    </div>
    <Transition name="fade">
      <Modal
      v-if="showModal"
      @close="closeModal"
      title="Выберите папку"
      :folders="mockFolders"
      @select="select"/>
    </Transition>
  </div>
</template>

<style scoped>
</style>
