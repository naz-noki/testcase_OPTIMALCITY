<template>
    <div class="popup">
        <div class="popup__block">
            <slot name="popup__close"></slot>
            <input 
            v-model="newValue"
            class="popup__inp"
            type="text" 
            placeholder="Введите новое значение value">
            <button class="popup__edit" @click="setNewValue">Сохранить</button>
        </div>
    </div>
</template>

<script setup>
  
  import { ref, defineEmits, } from 'vue';

  const emit = defineEmits(['addNewValue']);

  const newValue = ref('');

  const setNewValue = () => {
    if(newValue.value !== ''){
        emit('addNewValue', newValue.value);
    }
  }

</script>