<template>
  <div id="app">
    <img src="@/assets/media/logo.svg" alt="logo" id="logo">
    <open-page v-if="page===0" @next-page="nextPage"></open-page>
    <pick-rank v-if="page===1" @chosenRank="chosenRank"></pick-rank>
    <main-page v-if="page===2" :rank="rank" @next-page="nextPage"></main-page>
    <final-page v-if="page===3" @restart="restart"></final-page>
  </div>
</template>
 
<script>
import  OpenPage from "@/components/OpenPage";
import  PickRank from "@/components/PickRank";
import  MainPage from "@/components/MainPage";
import  FinalPage from "@/components/FinalPage";
export default {
  name: "app",
  components: {
    OpenPage,
    PickRank,
    MainPage,
    FinalPage
  },
  data() {
    return {
      page: 0,
      rank: ""
    }
  },
  methods: {
    nextPage() {
      this.page ++;
    },
    chosenRank(rank) {
      this.rank = rank;
      this.page++;
    },
    restart() {
      this.page = 0;
    }
  }
};
</script>

<style>
@font-face {
  font-family: "assistant-bold";
  src: url(assets/fonts/Assistant-Bold.otf);
}
@font-face {
  font-family: "assistant-extraBold";
  src: url(assets/fonts/Assistant-ExtraBold.otf);
}
@font-face {
  font-family: "assistant";
  src: url(assets/fonts/Assistant-Regular.otf);
}
#app {
  width: 100vw;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  position: absolute;
  color: #FFFFFF;
  top: 0;
  right: 0;
  direction: rtl;
  margin: 0px;
  font-family: "assistant";
  text-align: center;
  background: linear-gradient(135deg, #267C71, #245652, #202C2F, #202C2F,  #1F1E23, #1F1E23);
}
#logo {
  max-width: 100%;
  position: absolute;
  top: 1.5vh;
  right: 0.5vw;
  height: 10vh;
  z-index: 5;
}
.title {
    font-family: "assistant-extraBold";
    margin: auto;
    width: 80vw;
    margin-top: 7vh;
    font-size: 3.25vw;
    text-shadow: 1px 0px 3px #000000;
}
.next-btn {
  position: absolute;
  cursor: pointer;
  background-color: #444446;
  font-family: "assistant-bold";
  font-size: 1.7vw;
  border-radius: 1.75vh;
  bottom: 6vh;
  left: 2vw;
  width: fit-content;
  padding: 1%;
  transition: all 0.4s;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}
.next-btn:hover {
    transform: scale(0.9);
}
@media (max-width: 600px) {
  #logo {
    top: 1vh;
    right: 1.5vw;
    height: 7vh;
  }
  .title {
      margin-top: 7vh;
      font-size: 8vw;
  }
  .next-btn {
    font-size: 6vw;
    border-radius: 2vw;
    padding: 1vh;
    bottom: 3.5vh;
    left: 6vw;
    box-shadow: rgba(255, 255, 255, 0.1) 0px 1px 1px 0px inset, rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px;  }
  }
</style>