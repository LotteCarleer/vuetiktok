<script setup>
import VideoPlayer from './components/VideoPlayer/VideoPlayer.vue';
import VideoDetails from './components/VideoPlayer/VideoDetails.vue';
import Chat from './components/Chat/Chat.vue';

import { onMounted, ref } from 'vue';

let currentVideo = ref("");
let currentDescription = ref("");
let currentUsername = ref("");
let currentIndex = ref(0);
let videos = ref([]);

onMounted(() => {
  fetch('https://api.jsonbin.io/v3/b/670ccbfaad19ca34f8b81951')
    .then((response) => response.json())
    .then((data) => {
      videos.value = data.record.data.videos;
      currentVideo.value = data.record.data.videos[0].video;
      currentDescription.value = data.record.data.videos[0].description;
      currentUsername.value = data.record.data.videos[0].username;
    });
});


function playNext(){
  //check the index, take the next one, if its the last one, go back to the first one
  if(currentIndex.value < videos.value.length - 1) {
    currentIndex.value++;
  } else {
    currentIndex.value = 0;
  }
  currentVideo.value = videos.value[currentIndex.value].video;
  currentDescription.value = videos.value[currentIndex.value].description;
  currentUsername.value = videos.value[currentIndex.value].username;
};



function playPrev(){
  if(currentIndex.value > 0) {
    currentIndex.value--;
  } else {
    currentIndex.value = videos.value.length - 1;
  }
  currentVideo.value = videos.value[currentIndex.value].video;
  currentDescription.value = videos.value[currentIndex.value].description;
  currentUsername.value = videos.value[currentIndex.value].username;
};

</script>

<template>
<div class="tiktok">
  
  <div>
    <VideoPlayer @play-next="playNext" @play-prev="playPrev" :src="currentVideo" />
  </div>

  <div><VideoDetails :description="currentDescription" :username="currentUsername" />
    <Chat />
  </div>

</div>
</template>

<style scoped>

</style>