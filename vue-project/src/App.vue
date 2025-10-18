<script setup>
  import { ref } from 'vue'
  import axios from 'axios';

  const videoId = ref("0000")
  const youtube_static = "https://www.youtube.com/results?search_query=img+"
  const youtube_static_alt = "https://www.youtube.com/results?search_query=img_"
  async function generateVideoId() {
    videoId.value = String(Math.floor(Math.random() * 10000)).padStart(4, '0')
    captureVideo()
  }
  async function captureVideo() {
    const video_url = youtube_static+videoId.value
    console.log(video_url)
    const config = {
      method: 'get',
      maxBodyLength: Infinity,
      url: video_url,
      headers: {
        'Cookie': 'GPS=1; VISITOR_INFO1_LIVE=9QXrWwUBVPY; VISITOR_PRIVACY_METADATA=CgJDQRIEGgAgTA%3D%3D; YSC=ZoB6Mxwx7LM; __Secure-ROLLOUT_TOKEN=CMe64fK3-63rrwEQ-fKkhYGukAMY-fKkhYGukAM%3D'
      }
    }
    axios.request(config)
    .then((response) => {
      console.log(JSON.stringify(response.data));
    })
    .catch((error) => {
      console.log(error);
    })
  }
</script>

<template>
  <h1>YouTube Randomizer</h1>
  <p>
    Click the button, where will you land?
  </p>
  <button v-on:click="generateVideoId">Find Random Youtube Video</button>
  <p>{{videoId}}</p>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/m--18DYiAdU?si=NJkqKFsVB9DBamMA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</template>

<style scoped></style>
