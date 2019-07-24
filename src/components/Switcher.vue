<template>
  <div class="Switcher">
    <div class="switchBtn">
      <el-button type="primary" class="btn btn-primary" @click="home">home</el-button>
      <el-button type="primary" class="btn btn-primary" @click="toggleLive">{{ isLive ? 'to playback' : 'to live' }}</el-button>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    isLive() {
      return this.$route.name === 'live'
    }
  },
  methods: {
    toggleLive() {
      debugger
      if (this.isLive) {
        this.$router.push('/playback')
      } else {
        this.$router.push('/live')
      }
    },
    home() {
      this.$router.push('/HelloWorld')
    }
  }
}
</script>

<style scoped>
.switchBtn {
  text-align: center;
  position: absolute;
  right: 0px;
  top: 10px;
}
</style>
