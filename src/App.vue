<script setup>
import { ref } from 'vue';

const isEditing = ref(false);
const buttonText = ref('Editable button');
const image = ref({ src: '/edit.svg', alt: 'edit-icon' });

// переключить disabled кнопки
const isDisabled = ref(false);

const handleEditBtnClick = () => {
  isEditing.value = !isEditing.value;
  image.value = isEditing.value
    ? { src: '/save.svg', alt: 'save-icon' }
    : { src: '/edit.svg', alt: 'edit-icon' };
};
</script>

<template>
  <div class="container">
    <button class="btn" :class="{ edited: isEditing }" :disabled="isDisabled">
      <input class="text" type="text" :disabled="!isEditing" v-model="buttonText" maxlength="15" />
      <img v-if="!isEditing" src="/play.svg" alt="play-icon" class="img-play" />
    </button>
    <button class="btn-edit" @click="handleEditBtnClick()" v-if="!isDisabled">
      <img :src="image.src" :alt="image.alt" />
    </button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  min-width: 169px;
  align-items: center;
  gap: 8px;
}

.btn {
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 4px 12px 4px 8px;
  min-width: 137px;
  border: none;
  border-radius: 4px;
  background-color: var(--default);
}

.btn:hover,
.btn:hover .text {
  cursor: pointer;
  background-color: var(--hover);
}

.btn:active,
.btn:active .text {
  background-color: var(--pressed);
}

.text {
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 16px;
  color: var(--black);
  background-color: var(--default);
  outline: none;
  border: none;
  width: 97px;
  padding: 0;
}

.edited {
  outline: 1px solid var(--black);
  background-color: var(--white);
}

.edited:hover,
.edited:active,
.edited:hover .text,
.edited:active .text,
.edited .text {
  background-color: var(--white);
}

.btn:disabled .text,
.btn:disabled {
  pointer-events: none;
  color: var(--inactive);
  background-color: var(--white);
}

.btn:disabled .img-play {
  opacity: 0.3;
}

.btn-edit {
  padding: 4px;
  border-radius: 4px;
  background-color: var(--default);
  cursor: pointer;
  border: none;
  display: flex;
}

.btn-edit:hover {
  background-color: var(--hover);
}

.btn-edit:active {
  background-color: var(--pressed);
}
</style>
