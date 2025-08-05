<template>
  <div id="fight-data">
    <div class="title">{{ title }}</div>
    <div class="subtitle">{{ subtitle }}</div>
    <div class="info-container">
      <div class="topic-container" v-for="(image, index) in imgList" :key="index">
        <img :src="image" alt="icon" class="img"/>
        <div class="txt">{{ txtList[index] }}</div>
      </div>
    </div>
    <div class="next-btn" @click="nextPage">הבנו</div>
  </div>
</template>

<script>
import json from "../../text.json";
import clock from "@/assets/media/clock.svg";
import bandaid from "@/assets/media/bandaid.svg";
import drop from "@/assets/media/drop.svg";
import timer from "@/assets/media/timer.svg";

export default {
  name: "fight-data",
  data() {
    return {
      title: json["fight-data"]["title"],
      subtitle: json["fight-data"]["subtitle"],
      imgList: [clock, bandaid, drop, timer], 
      txtList: json["fight-data"]["txt-list"]
    };
  },
  methods: {
    nextPage () {
        this.$emit('next-page');
    }
  }
};
</script>

<style scoped>
#fight-data {
  height: 100vh;
  overflow: hidden;
  width: 100vw;
}

.subtitle {
  text-shadow: 1px 0px 3px #000000;
  font-size: 2.5vw;
  margin-top: 0.25vh;
}

.info-container {
    display: flex;
    flex-wrap: nowrap;
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
    position: relative;
    width: 100%;
}
.topic-container {
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 22%;
    margin: 1%;
}
.img {
    max-width: 100%;
    height: 20vh;
    margin-bottom: 0vh;
}
.txt {
    padding: 0%;
    width: 90%;
    font-size: 1.75vw;
    text-align: start;
    white-space: break-spaces;
}

@media (max-width: 600px) {
  .subtitle {
    font-size: 6vw;
    margin-top: 0.25vh;
  }
  .info-container {
    margin-top: 2vh;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    position: static;
    width: 100%;
   }
   .topic-container {
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        height: 15vh;
        margin: 1%;
        width: 100%;
    }
    .img {
        width: 25vw;
        height: auto;
        max-height: 100%;
    }
    .txt {
        font-size: 4.5vw;
        width: 60vw;
    }

}
</style>
