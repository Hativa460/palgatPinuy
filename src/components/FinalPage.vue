<template>
  <div id="final-page">
    <div id="centering-div">
      <div id="big-title">זהו עברנו על הכל:)</div>
      <div id="small-title">נו מה אומר, בא לך עוד הפעם?</div>
      <img src="@/assets/media/restart.svg" alt="again" id="restart" @click="restart" />
    </div>
  </div>
</template>

<script>
export default {
  name: "final-page",
  methods: {
    restart() {
      this.$emit("restart");
    },

    createSparkle(x, y, options = {}) {
      const sparkle = document.createElement("div");
      const shapeIndex = Math.floor(Math.random() * 2); // 0 = circle, 1 = star
      sparkle.className = `sparkle sparkle-${shapeIndex}`;

      const size = options.size || 5 + Math.random() * 15;
      sparkle.style.width = `${size}px`;
      sparkle.style.height = `${size}px`;
      sparkle.style.left = `${x}px`;
      sparkle.style.top = `${y}px`;

      const duration = options.duration || 300 + Math.random() * 600;
      sparkle.style.animationDuration = `${duration}ms`;
      sparkle.style.animationTimingFunction = ["ease", "ease-in", "ease-out", "linear"][Math.floor(Math.random() * 4)];

      if (options.burst) {
        const angle = Math.random() * 2 * Math.PI;
        const distance = 40 + Math.random() * 80;
        const dx = Math.cos(angle) * distance;
        const dy = Math.sin(angle) * distance;
        sparkle.style.setProperty("--dx", `${dx}px`);
        sparkle.style.setProperty("--dy", `${dy}px`);
        sparkle.classList.add("burst");
      } else {
        sparkle.style.setProperty("--dy", `${-20 - Math.random() * 40}px`);
        sparkle.style.setProperty("--scale", `${1 + Math.random() * 0.5}`);
        sparkle.style.setProperty("--rotate", `${Math.random() * 360}deg`);
      }

      document.body.appendChild(sparkle);
      setTimeout(() => sparkle.remove(), 1200);
    },

    handleMouseMove(event) {
      if (window.innerWidth <= 600) return;
      if (event.target.closest('#restart')) return; // ❌ Don't sparkle over restart

      for (let i = 0; i < 5; i++) {
        const offsetX = (Math.random() - 0.5) * 30;
        const offsetY = (Math.random() - 0.5) * 30;
        this.createSparkle(event.pageX + offsetX, event.pageY + offsetY);
      }
    },

    handleClick(event) {
      if (window.innerWidth <= 600) return;
      if (event.target.closest('#restart')) return; // ❌ No sparkles on restart click

      for (let i = 0; i < 15; i++) {
        this.createSparkle(event.pageX, event.pageY, { burst: true });
      }
    },
  },

  mounted() {
    window.addEventListener("mousemove", this.handleMouseMove);
    window.addEventListener("click", this.handleClick);
  },
  beforeDestroy() {
    window.removeEventListener("mousemove", this.handleMouseMove);
    window.removeEventListener("click", this.handleClick);
  },
};
</script>

<style scoped>
#final-page {
  height: 100%;
  overflow-x: hidden;
  width: 100vw;
}

#centering-div {
  position: absolute;
  top: 50%;
  right: 50%;
  transform: translate(50%, -50%);
}

#big-title {
  font-family: "assistant-extraBold";
  font-size: 4.25vw;
  margin-bottom: 2vh;
}

#small-title {
  font-family: "assistant-bold";
  font-size: 3vw;
  margin-bottom: 2vh;
}

#restart {
  max-width: 100%;
  height: 20vh;
  cursor: pointer;
}

@media (max-width: 600px) {
  #big-title {
    font-size: 10vw;
    margin-bottom: 2vh;
    width: 100vw;
  }

  #small-title {
    font-size: 8vw;
    margin-bottom: 2vh;
  }

  #restart {
    max-width: 100%;
    height: 15vh;
    cursor: pointer;
  }
}
</style>

<!-- Global Sparkle Styles -->
<style>
.sparkle {
  position: absolute;
  pointer-events: none;
  opacity: 0.9;
  transform: translate(-50%, -50%);
  z-index: 9999;
  animation-fill-mode: forwards;
  background-color: #36e9a0;
}

/* Circle */
.sparkle-0 {
  border-radius: 50%;
}

/* Star */
.sparkle-1 {
  clip-path: polygon(
    50% 0%,
    61% 35%,
    98% 35%,
    68% 57%,
    79% 91%,
    50% 70%,
    21% 91%,
    32% 57%,
    2% 35%,
    39% 35%
  );
}

/* Trail Animation */
.sparkle:not(.burst) {
  animation-name: sparkleFloat;
}

@keyframes sparkleFloat {
  0% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1) rotate(0deg);
  }
  100% {
    opacity: 0;
    transform: translate(-50%, var(--dy)) scale(var(--scale, 1)) rotate(var(--rotate, 0deg));
  }
}

/* Burst Animation */
.burst {
  animation-name: sparkleBurst;
}

@keyframes sparkleBurst {
  0% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1) rotate(0deg);
  }
  100% {
    opacity: 0;
    transform: translate(calc(-50% + var(--dx)), calc(-50% + var(--dy))) scale(0.5) rotate(360deg);
  }
}
</style>
