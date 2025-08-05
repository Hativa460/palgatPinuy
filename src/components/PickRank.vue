<template>
  <div id="pick-rank">
    <div class="title">רגע לפני שמתחילים, סמן מי אתה</div>
    <div class="flex-container">
      <div class="rankOpt" @click="triggerShine($event)" id="mm">
        <img src="@/assets/media/ממ.svg" alt="">
      </div>
      <div class="rankOpt" @click="triggerShine($event)" id="mp">
        <img src="@/assets/media/מפ.svg" alt="">
      </div>
      <div class="rankOpt" @click="triggerShine($event)" id="mgd">
        <img src="@/assets/media/מגד.svg" alt="">
      </div>
    </div>
    <div class="next-btn" @click="nextPage">שנתחיל?</div>
  </div>
</template>

<script>
export default {
  name: "pick-rank",
  data() {
    return {
      chosenRank: ""
    };
  },
  methods: {
    triggerShine(event) {
      this.chosenRank = event.currentTarget.id;
      // Remove chosenRank from all options
      const rankOptions = document.getElementsByClassName("rankOpt");
      for (let i = 0; i < rankOptions.length; i++) {
        rankOptions[i].classList.remove("chosenRank");
      }
      // Add chosenRank to current
      const el = event.currentTarget;
      el.classList.add("chosenRank");

      // Trigger shine animation only on touch devices
      if ('ontouchstart' in window || navigator.maxTouchPoints > 0) {
        el.classList.remove('shine-animate');
        void el.offsetWidth; // force reflow
        el.classList.add('shine-animate');
      }
    },
    nextPage() {
      if (this.chosenRank === "") {
        alert("כל הכבוד על ההתלהבות להתקדם אבל קודם תבחר תפקיד");
      } else {
        this.$emit("chosenRank", this.chosenRank);
      }
    }
  }
};
</script>

<style scoped>
#pick-rank {
  height: 100vh;
  overflow: hidden;
  width: 100vw;
}

.flex-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100%;
  position: absolute;
  top: 50%;
  right: 50%;
  transform: translate(50%, -50%);
  /* margin-top: 5%; */
}

.rankOpt {
  position: relative;
  width: 25vw;
  margin: 3%;
  display: inline-block;
  overflow: hidden;
  cursor: pointer;
}

.chosenRank {
  scale: 1.1;
  filter: drop-shadow(0px 0px 1.8vh #d3e3fa);
}

.rankOpt img {
  width: 100%;
  height: auto;
  display: block;
  transition: opacity 0.3s ease;
}

.rankOpt::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: -75%;
  width: 50%;
  height: 77%;
  background: linear-gradient(
    120deg,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0) 25%,
    rgba(255, 255, 255, 0.5) 50%,
    rgba(255, 255, 255, 0) 75%,
    rgba(255, 255, 255, 0) 100%
  );
  opacity: 0;
  pointer-events: none;
  will-change: left, opacity;
}

/* Hover effect on large screens only */
@media (min-width: 601px) {
  .rankOpt:hover::after {
    animation: shineMove 0.8s ease-in-out;
    opacity: 1;
  }
  .rankOpt:hover img {
    opacity: 0.85;
  }
}

/* Shine animation triggered by JS */
.rankOpt.shine-animate::after {
  animation: shineMove 0.8s ease-in-out;
  opacity: 1;
}

@keyframes shineMove {
  0% {
    left: -75%;
  }
  100% {
    left: 125%;
  }
}

@media (max-width: 600px) {
  .flex-container {
    flex-direction: column;
  }
  .rankOpt {
    width: 65vw;
    user-select: none;
  }
}
</style>
