<template>
    <div id="nav-bar">
        <div class="close" @click="closeMenu"></div>
        <div class="topics-container">
            <div v-for="(topic, index) in navTopics" :key="index" class="topic" :class="index === topicNum ? 'currTopic' : ''" @click="switchPage(index)">{{topic}}</div>
        </div>
    </div>
</template>

<script>
import json from "../../text.json";
export default {
    name: "nav-bar",
    props: ["rank", "topicNum"],
    data() {
        return {
            navTopics: json.navTopics[this.rank]
        }
    },
    methods: {
        closeMenu() {
            this.$emit('close-menu');
        },
        switchPage(index) {
            this.$emit('switchPage', index);
        }
    }
}
</script>

<style scoped>
    @keyframes moving {
   from {
    margin-right: -70vw;
   } 
   to {
    margin-right: 0px;
   } 
}
@-webkit-keyframes moving {
    from {
    margin-right: -70vw;
   } 
   to {
    margin-right: 0px;
   } 
}

@keyframes closeMenu {
    from {
        margin-right: 0px;
    }
    to {
        margin-right: -70vw;
    }
}
@-webkit-keyframes closeMenu {
    from {
        margin-right: 0px;
    }
    to {
        margin-right: -70vw;
    }
}
#nav-bar {
    position: absolute;
    left: 0px;
    top: 0px;
    margin: 0px;
    height: 100%;
    width: 25vw;
    z-index: 5;
    background-color: white;
    color: #1F1F24;
    animation: moving 500ms ease-in-out;
    -webkit-animation: moving 500ms ease-in-out ;
}
.topics-container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-evenly;
    padding-right: 1vw;
    width: 80%;
    height: 100%;
}
.topic {
    font-size: 2.2vw;
    cursor: pointer;
    text-align: start;
}
.currTopic {
    font-family: "assistant-extraBold";
}

.close {
  position: absolute;
  top: 2%;
  left: 1%;
  width: 5vw;
  min-height: 8vh;
  overflow: hidden;
  padding: 2%;
    cursor: pointer;
}

.close:before, .close:after {
  position: absolute;
  left: 5%;
  top: 40%;
  content: ' ';
  height: 1.75vh;
  width: 4vw;
  background-color: #1F1F24;
  border-radius: 0.25vw;
}
.close:before {
  transform: rotate(45deg);
}
.close:after {
  transform: rotate(-45deg);
}
@media (max-width: 600px) {
    #nav-bar {
        width: 70vw;
    }
    .topic {
        font-size: 7.3vw;
    }
    .close {
        position: absolute;
        top: 2%;
        left: 2%;
        width: 10vw;
        height: 10vh;
        overflow: hidden;
        padding: 2%;
    }
    .close:before, .close:after {
        position: absolute;
        left: 5%;
        top: 20%;
        content: ' ';
        height: 1vh;
        width: 10vw;
        background-color: #1F1F24;
        border-radius: 0.5vw;
    }
}
</style>