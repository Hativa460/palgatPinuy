<template>
    <div id="pointers">
        <div class="title">{{ title }}</div>
        <div class="blocks-container">
            <div v-for="(block, index) in blocks" :key="index" class="block">
                <div class="block-title">{{ block.title }}</div>
                <div class="step" v-for="(subtitle, i) in block.subtitles" :key="`sub-${index}-${i}`">
                    <div class="title-container">
                        <img 
                            src="../assets/media/plus.svg" 
                            alt="plus" 
                            class="plus" 
                            v-if="!pressedIndex.includes(`${index}-${i}`)" 
                            @click="showText(index, i)"
                        >
                        <img 
                            src="../assets/media/minus.svg" 
                            alt="minus" 
                            class="plus" 
                            v-if="pressedIndex.includes(`${index}-${i}`)" 
                            @click="showText(index, i)"
                        >
                        <div class="step-title">{{ subtitle }}</div>
                    </div>
                    <div class="extra-txt" v-if="pressedIndex.includes(`${index}-${i}`)">
                        {{ block.extra[i] }}
                    </div>
                </div>
            </div>
        </div>
        <div class="next-btn" @click="nextPage">שנתקדם?</div>
    </div>
</template>

<script>
import json from "../../text.json";

export default {
    name: "pointers",
    data() {
        return {
            title: json["pointers"]["title"],
            blocks: json["pointers"]["blocks"],
            pressedIndex: []
        };
    },
    methods: {
        showText(blockIdx, subtitleIdx) {
            const key = `${blockIdx}-${subtitleIdx}`;
            if (this.pressedIndex.includes(key)) {
                this.pressedIndex = this.pressedIndex.filter(i => i !== key);
            } else {
                this.pressedIndex = [...this.pressedIndex, key];
            }
        },
        nextPage () {
            this.$emit('next-page');
        }
    }
};
</script>

<style scoped>
#pointers {
    height: fit-content;
    min-height: 100vh;
    overflow-x: hidden;
    overflow-y: scroll;
    width: 100vw;
}
.blocks-container {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    width: 100%;
    align-items: flex-start;
    justify-content: space-evenly;
    margin-top: 5vh;
}
.block {
    border: solid 0.5vh white;
    border-radius: 2vw;
    border-top: none;
    width: 35vw;
    min-height: 40vh;
    padding: 1%;
    padding-top: 0%;
}
.block-title {
    font-family: "assistant-extraBold";
    font-size: 2.5vw;
    margin-top: -2.75vh;
}
.title-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    margin-top: 0.5vh;
    margin-bottom: 0.5vh;
}
.step-title {
    font-family: "assistant-bold";
    font-size: 2vw;
}
.plus {
    max-width: 100%;
    margin-left: 1vw;
    cursor: pointer;
    height: 4.2vh;
}
.extra-txt {
    text-align: start;
    font-size: 1.75vw;
    margin-right: 3vw;
}
@media (max-width: 600px) {
    .blocks-container {
        flex-direction: column;
        width: 100%;
        align-items: center;
        justify-content: flex-start;
        margin-top: 5vh;
    }

    .block {
        border: solid 0.5vh white;
        border-radius: 2vh;
        border-top: none;
        width: 80vw;
        min-height: auto;
        padding: 1%;
        padding-top: 0%;
        margin-bottom: 5vh;
    }
    .block-title {
        font-family: "assistant-extraBold";
        font-size: 5vw;
        margin-top: -2vh;
    }
    .title-container {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        margin-top: 0.75vh;
        margin-bottom: 0.75vh;
    }
    .step-title {
        font-size: 4vw;
    }
    .extra-txt {
        text-align: start;
        font-size: 3.75vw;
        margin-right: 3vw;
    }
    .next-btn {
        position: static;
        margin-top: 1.5vh;
        margin-right: 70vw;
        margin-bottom: 3vh;
    }
}
</style>
