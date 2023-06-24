<template>
  <div class="mainPage">

    <ul class="postsList">
      <li 
      v-for="(post, idx) of posts"
      :key="idx"
      class="postsList__item"
      >
        <div class="postsList__item_info">
          name: {{ post.name }} <br>
          value: {{ post.value }}
        </div>
        <button class="postsList__item_edit" @click="getIdForNewValue(idx)">
          <img src="../assets/img/icons8-редактировать-50.png" alt="" class="edit__img">
        </button>
      </li>
    </ul>

    <editPopup v-if="visiblePopup" @addNewValue="getNewValue">
      <template #popup__close>
        <button class="popup__close" @click="addVisibleToPopup">
          X
        </button>
      </template>
    </editPopup >

  </div>
</template>

<script setup>
  
  import { ref, } from 'vue';

  import PostsFromData from '../state/data';

  import editPopup from './editPopup.vue';

  const visiblePopup = ref(false);

  const posts = ref([...PostsFromData]);
  const id = ref();

  const addVisibleToPopup = () => {
    visiblePopup.value ?  visiblePopup.value = false :  visiblePopup.value = true;
  }

  const getIdForNewValue = (idx) => {
    addVisibleToPopup();
    id.value = idx;
  }

  const getNewValue = (newValue) => {
    posts.value[id.value].value = newValue;
  }

</script>