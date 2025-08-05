<template>
    <div id="event-steps">
        <div class="title">{{title}}</div>
        <div class="steps-container">
            <div class="step-container" v-for="(step, index) in steps" :key="index">
                <div class="number">{{index+1}}.</div>
                <div class="txt">{{step}}</div>
            </div>
        </div>
        <div class="next-btn" @click="nextPage">נדיר בואו נתקדם</div>
    </div>
</template>

<script>
    import json from "../../text.json";
    export default {
        name: "event-steps",
        data() {
            return {
                title: json["event-steps"]["title"],
                steps: json["event-steps"].steps
            }
        },
        methods: {
            nextPage () {
                this.$emit('next-page');
            }
        }
    }
</script>

<style scoped>
#event-steps {
    height: 100vh;
    overflow: hidden;
    width: 100vw;
}
.steps-container {
    display: flex;
    flex-wrap: nowrap;
    flex-direction: row;
    margin: auto;
    width: 80%;
    position: absolute;
    top: 50%;
    right: 50%;
    transform: translate(50%, -50%);
    /* margin-top: 2vh; */
    align-items: flex-start;
    justify-content: space-between;
}
.step-container {
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    width: 30%;
}
.number {
    text-align: start;
    font-size: 10vw;
    font-family: "assistant-extraBold";
    color: #36E9A0;
}
.txt {
    font-size: 2.5vw;
    padding-left: 10%;
    text-align: start;
}
@media (max-width: 600px) {
    .steps-container {
        flex-direction: column;
        margin: auto;
        width: 80vw;
        margin-top: 2vh;
        align-items: center;
        height: 50%;
        justify-content: space-between;
        position: relative;
        right: 0%;
        top: 0%;
        transform: none;
    }
    .step-container {
        flex-direction: row;
        width: 100%;
        justify-content: flex-start;
        align-items: center;
    }
    .number {
        font-size: 10vh;
        margin-left: 5%;
    }
    .txt {
        font-size: 7vw;
        padding-left: 0%;
    }
}
</style>