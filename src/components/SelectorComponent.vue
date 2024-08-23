<template>
  <div class="item-selector">
    <!-- Верхний блок -->
    <div class="top-section">
      <div class="selected-items">
        <div v-for="item in selectedUserItems" :key="item.id" class="item">
          {{ item.name }}
        </div>
        <p>selected: {{ selectedUserItems.length }} / 6</p>
      </div>
      <div class="selected-item">
        <div v-if="selectedItem" class="item">
          {{ selectedItem.name }}
        </div>
      </div>
    </div>

    <!-- нижний блок -->
    <div class="bottom-section">
      <div class="user-items">
        <div v-for="item in userItems" :key="item.id" class="item" @click="toggleUserItem(item)">
          {{ item.name }}
        </div>
      </div>
      <div class="selectable-items">
        <div v-for="item in selectableItems" :key="item.id" class="item" @click="selectItem(item)">
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const userItems = ref([
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' }
]);

const selectableItems = ref([
  { id: 11, name: 'Jacket 1' },
  { id: 12, name: 'Jacket 2' },
  { id: 13, name: 'Jacket 3' },
  { id: 14, name: 'Jacket 4' },
  { id: 15, name: 'Hoodie 1' },
  { id: 16, name: 'Hoodie 2' },
  { id: 17, name: 'Hoodie 3' },
  { id: 18, name: 'Hoodie 4' }
]);

const selectedUserItems = ref([]);
const selectedItem = ref(null);

// функция для выбора вещи из левого блока
function toggleUserItem(item) {
  const index = selectedUserItems.value.findIndex(i => i.id === item.id);
  if (index !== -1) {
    selectedUserItems.value.splice(index, 1);
  } else if (selectedUserItems.value.length < 6) {
    selectedUserItems.value.push(item);
  }
}

// функция для выбора вещь из правого блока
function selectItem(item) {
  selectedItem.value = item;
}
</script>

<style scoped>
.item-selector {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.top-section {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.bottom-section {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.user-items, .selectable-items {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.item {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
  text-align: center;
  width: 100px;
}

.selected-items p {
  margin-top: 10px;
}
</style>