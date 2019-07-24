<template>
  <div class="liveView">
    <h3>Vue Video.js Live Demo</h3>
    <p>Current Stream:
      <span class="badge badge-success">{{ currentStream }}</span>
    </p>
    <p>Current Tech:
      <span class="badge badge-info">{{ currentTech }}</span>
    </p>
    <video-player ref="videoPlayer" class="vjs-custom-skin" :options="playerOptions" @play="onPlay" @ready="onPlayerReadied" @timeupdate="onTimeupdate" />
    <div class="selectWrapper">
      Switch Tech：
      <div class="form-check">
        <input id="html5" v-model="currentTech" class="form-check-input" type="radio" name="tech" value="Html5" @change="changeTech">
        <label class="form-check-label" for="html5">
          Html5
        </label>
      </div>
      <div class="form-check">
        <input id="flash" v-model="currentTech" class="form-check-input" type="radio" name="tech" value="Flash" @change="changeTech">
        <label class="form-check-label" for="flash">
          Flash
        </label>
      </div>
    </div>

    <h5>Enter your streams link below</h5>
    <div class="inputWrapper">
      <div v-if="currentStream==='RTMP'" class="form-group row">
        <label class="col-sm-4 col-form-label">RTMP: </label>
        <div class="col-sm-8">
          <input v-model="streams.rtmp" class="form-control" type="text" placeholder="RTMP url here">
        </div>
      </div>
      <div v-else class="form-group row">
        <label class="col-sm-4 col-form-label">HLS: </label>
        <div class="col-sm-8">
          <input v-model="streams.hls" class="form-control" type="text" placeholder="HLS url here">
        </div>
      </div>
    </div>
    <div class="buttonWrapper">
      <button class="btn btn-primary" type="button" @click="enterStream">Apply</button>
    </div>

    <Switcher />
  </div>
</template>

<script>
import Switcher from '@/components/Switcher'

const isProduction = process.env.NODE_ENV === 'production'

export default {
  name: 'Live',
  components: {
    Switcher
  },
  data() {
    return {
      initialized: false,
      currentTech: '',
      streams: {
        rtmp: '',
        hls: ''
      },
      playerOptions: {
        overNative: true,
        autoplay: false,
        controls: true,
        techOrder: ['flash', 'html5'],
        sourceOrder: true,
        flash: {
          hls: { withCredentials: false },
          swf: '../../assets/media/video-js.swf'
        },
        html5: { hls: { withCredentials: false }},
        sources: [
          {
            withCredentials: false,
            type: 'rtmp/mp4',
            src: 'rtmp://184.72.239.149/vod/&mp4:BigBuckBunny_115k.mov'
          },
          {
            withCredentials: false,
            type: 'application/x-mpegURL',
            src: 'http://playertest.longtailvideo.com/adaptive/bipbop/gear4/prog_index.m3u8'
          }
        ],
        poster: isProduction ? '/cdv-cloud-web/src/assets/images/logo.png' : '../../assets/images/logo.png'
        // controlBar: {
        //   timeDivider: false, // 时间分割线
        //   durationDisplay: false, // 总时间
        //   progressControl: true, // 进度条
        //   customControlSpacer: true, // 未知
        //   fullscreenToggle: true // 全屏
        // },
      }
    }
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player
    },
    currentStream() {
      return this.currentTech === 'Flash' ? 'RTMP' : 'HLS'
    }
  },
  methods: {
    onPlay() {
      debugger
    },
    onPlayerReadied() {
      if (!this.initialized) {
        this.initialized = true
        this.currentTech = this.player.techName_
      }
    },
    // record current time
    onTimeupdate(e) {
      console.log('currentTime', e.cache_.currentTime)
    },
    enterStream() {
      this.playerOptions.sources[1].src = this.streams.hls
      this.playerOptions.sources[0].src = this.streams.rtmp
      this.playerOptions.autoplay = true
    },
    changeTech() {
      if (this.currentTech === 'Html5') {
        this.playerOptions.techOrder = ['html5']
      } else if (this.currentTech === 'Flash') {
        this.playerOptions.techOrder = ['flash']
      }
      this.playerOptions.autoplay = true
    }
  }
}
</script>

<style scoped>
.liveView {
  position: relative;
  text-align: center;
}

.selectWrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  line-height: 30px;
  margin: 20px;
  vertical-align: baseline;
}

.inputWrapper {
  width: 500px;
  margin: 0 auto;
}

.buttonWrapper {
  text-align: center;
}
</style>
