<template>
  <div id="demonstrations">
    <div class="title">{{ title }}</div>
    <div class="carusel-wrapper">
      <div class="arrow" @click="togglePhoto">&#8249;</div>
      <div id="media-wrapper">
        <video
          v-if="currPic === 1"
          :src="require('@/assets/media/dem1.mp4')"
          muted
          loop
          controls
        ></video>
        <img
          v-else
          :src="require('@/assets/media/dem2.png')"
          alt="demonstration"
        />
      </div>
      <div class="arrow" @click="togglePhoto">&#8250;</div>
    </div>
    <div class="next-btn" @click="nextPage">כן כן ראיתי</div>
  </div>
</template>

<script>
import json from "../../text.json";

export default {
  name: "demonstrations",
  data() {
    return {
      title: json["demonstrations"]["title"],
      currPic: 1,
    };
  },
  methods: {
    nextPage() {
      this.$emit("next-page");
    },
    togglePhoto() {
      this.currPic = this.currPic === 1 ? 2 : 1;
    },
  },
};
</script>

<style scoped>
#demonstrations {
  height: 100vh;
  width: 100vw;
  overflow-x: hidden; /* only hide horizontal, not vertical */
  overflow-y: visible;
}

.carusel-wrapper {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  padding: 2vh 0;
}

.arrow {
  color: #36E9A0;
  font-size: 8vw;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
  user-select: none;
  /* line-height: 1; */
  width: 10vw;
  height: 70vh; /* same as media height */
  display: flex;
  align-items: center;
  justify-content: center;
}


#media-wrapper {
  width: 60vw;
  height: 70vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #00000010;
  border-radius: 10px;
  overflow: hidden;
}

video,
img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
@media (max-width: 600px) {
    .arrow {
        color: #36E9A0;
        font-size: 15vw;
        font-family: Arial, Helvetica, sans-serif;
        cursor: pointer;
        user-select: none;
        /* line-height: 1; */
        /* width: 5vw; */
        height: 40vh; /* same as media height */
        display: flex;
        align-items: center;
        justify-content: center;
    }

    #media-wrapper {
        width: 85vw;
        height: 40vh;
        display: flex;
        align-items: center;
        justify-content: center;
        background: #00000010;
        border-radius: 10px;
        overflow: hidden;
    }
    .carusel-wrapper {
        position: absolute;
        top: 50%;
        right: 50%;
        transform: translate(50%, -50%);
    }
}
</style>
