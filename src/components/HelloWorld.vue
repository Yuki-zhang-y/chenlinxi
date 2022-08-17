<template>
  <div class="hello">
    <div class="box">
      <img src="@/assets/invite3.jpg" alt="">
      <!-- <audio src="/public/music/music.mp3" controls autoplay loop="loop"></audio> -->
    </div>
    <audio id="music-audio" autoplay preload="auto" loop>
      <source src="@/assets/music.mp3" type="audio/mpeg">
    </audio>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    audioAutoPlay() {
      var audio = document.getElementById('music-audio');
      audio.play();
      document.addEventListener("WeixinJSBridgeReady", function () {
        audio.play();
      }, false);
    },
    // 音乐播放
    autoPlayMusic() {
      // 自动播放音乐效果，解决浏览器或者APP自动播放问题
      function musicInBrowserHandler() {
        this.musicPlay(true);
          document.body.removeEventListener('touchstart', musicInBrowserHandler);
        }
        document.body.addEventListener('touchstart', musicInBrowserHandler);
        // 自动播放音乐效果，解决微信自动播放问题
        function musicInWeixinHandler() {
        this.musicPlay(true);
        document.addEventListener("WeixinJSBridgeReady", function () {
          this.musicPlay(true);
        }, false);
        document.removeEventListener('DOMContentLoaded', musicInWeixinHandler);
      }
      document.addEventListener('DOMContentLoaded', musicInWeixinHandler);
    },
    musicPlay(isPlay) {
      var media = document.querySelector('#music-audio')
      if(isPlay && media.paused) {
        media.play()
      }
      if (!isPlay && !media.paused) {
        media.pause();
      }
    },
  },
  mounted() {
    this.autoPlayMusic();
    this.audioAutoPlay();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
.box {
  height: 100vh;
  display: flex;
  align-items: flex-start;
  
}
img {
  width: 100%;
  margin-top: 30px;
}
</style>
