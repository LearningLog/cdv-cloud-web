<template>
  <div class="playbackView">
    <h3>Vue Video.js Playback Demo</h3>
    <p>Current Type: <span class="badge badge-success">mp4</span></p>
    <video-player ref="videoPlayer" class="vjs-custom-skin" :options="playerOptions" />

    <div class="optionsWrapper">
      <div class="form-group row">
        <label class="col-sm-4 col-form-label">Playback: </label>
        <div class="col-sm-8">
          <input v-model="url" class="form-control" type="text" placeholder="playback url here">
        </div>
        <div class="w-100 mt-3 text-center">
          <button class="btn btn-primary" @click="handleApply">apply</button>
        </div>
      </div>
    </div>

    <Switcher />
  </div>
</template>

<script>
import Switcher from '@/components/Switcher'
export default {
  name: 'Playback',
  components: {
    Switcher
  },
  data() {
    return {
      url: '',
      playerOptions: {
        autoplay: false,
        controls: true,
        sources: [{
          type: 'video/mp4',
          src: 'https://cdn.theguardian.tv/webM/2015/07/20/150716YesMen_synd_768k_vp8.webm'
          // src: "http://www.html5videoplayer.net/videos/madagascar3.mp4"
        }]
      }
    }
  },
  methods: {
    handleApply() {
      this.playerOptions.sources[0].src = this.url
    }
  }
}
</script>

<style scoped>
.playbackView {
  position: relative;
  text-align: center;
}

.optionsWrapper {
  width: 500px;
  margin: 20px auto;
}
</style>
