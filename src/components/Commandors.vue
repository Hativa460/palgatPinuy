<template>
  <div id="commandors">
    <div class="title">{{ title }}</div>
    <div class="pics-container">
      <img
        v-for="(src, index) in resolvedPics"
        :key="index"
        :src="src"
        alt="pic"
        class="pic"
      />
    </div>
    <div class="next-btn" @click="nextPage">נדיר בואו נתקדם</div>
  </div>
</template>

<script>
import json from "../../text.json";

export default {
  name: "commandors",
  props: ["rank"],
  data() {
    return {
      title: json["commandors"].title,
      pics: json["commandors"].pics,
      picsmm: json["commandors"].picsmm,
    };
  },
  computed: {
    resolvedPics() {
      const list = this.rank === "mm" ? this.picsmm : this.pics;
      return list.map(pic => require(`@/assets/media/${pic}`));
    },
  },
  methods: {
    nextPage() {
      this.$emit("next-page");
    },
  },
};
</script>

<style scoped>
#commandors {
  height: 100vh;
  overflow: hidden;
  width: 100vw;
}

.pics-container {
  display: flex;
  /* margin-top: 1.5vh; */
  flex-direction: row;
  align-items: center;
  width: 100vw;
  justify-content: space-evenly;
  position: absolute;
  top: 50%;
  right: 50%;
  transform: translate(50%, -50%);
}

.pic {
  max-height: 100%;
  width: 30vw;
}

@media (max-width: 600px) {
  .pics-container {
    flex-direction: column;
  }
  .pic {
    width: 70vw;
    margin: 0.5vh 0;
  }
}
</style>
