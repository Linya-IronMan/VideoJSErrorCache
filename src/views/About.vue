<template>
  <div class="about">
    <h1>This is an about page</h1>
    <video
      ref="videoPlayer"
      id="videoPlayer"
      class="video-js video-editor-video"
      controlsw
      :src="curRow.url"
    ></video>
    <button @click="play"> play </button>
    <button @click="pause"> pause </button>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import videojs from "video.js";
import "video.js/dist/video-js.css";


@Component({
  components: {},
})
export default class Home extends Vue {
  
  private play() {

    console.log("play", this.player.paused());
    (this.$refs.videoPlayer as any).play();
    this.player.play();
  }
  private pause() {
    console.log("pause", this.player.paused());
    (this.$refs.videoPlayer as any).pause();
    this.player.pause();
  }
  private curRow = {
    url: "http://172.31.93.168:8081/test.mp4"
  }
  private options: any = {
    autoplay: true,
    controls: true,
    controlBar: {
      children: [
        { name: "playToggle" }, // 播放按钮
        { name: "currentTimeDisplay" }, // 当前已播放时间
        { name: "progressControl" }, // 播放进度条
        { name: "durationDisplay" }, // 总时间
        {
          // 倍数播放
          name: "playbackRateMenuButton",
          playbackRates: [0.5, 1, 1.5, 2, 2.5],
        },
        {
          name: "volumePanel", // 音量控制
          inline: false, // 不使用水平方式
        },
        { name: "FullscreenToggle" }, // 全屏
      ],
    },
  };

  private player:any ;
  mounted() {
    this.player = videojs(this.$refs.videoPlayer, this.options);
    console.log(this.player, "=====");

    (this.$refs.videoPlayer as any).addEventListener("click", () => {

      if (this.player.paused()) {
        this.play();
      } else {
        this.pause();
      }
    });
    this.player.on("play", () => {
      console.log("play");
    })
  }
}
</script>