<template>
    <div id="treatment-ability">
        <div class="title">{{title}}</div>
        <div class="steps-container">
            <div v-for="(step, index) in steps" :key="index" class="step-container">
                <div class="number">{{ index + 1 }}
                </div>
            <div class="step">
                    {{ step }}
            </div>
            </div>
        </div>
        <div class="next-btn" @click="nextPage">יאללה ממשיכים</div>
    </div>
</template>

<script>
    import json from "../../text.json";
    export default {
        name: "treatment-ability",
        data() {
            return {
                title: json["treatment-ability"]["title"],
                steps: json["treatment-ability"]["steps"]
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
#treatment-ability {
    height: 100vh;
    overflow: hidden;
    width: 100vw;
}
.steps-container {
    display: flex;
    flex-direction: row;
    margin: auto;
    position: absolute;
    top: 50%;
    right: 50%;
    transform: translate(50%, -50%);
    /* margin-top: 3%; */
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: stretch;
    width: 90%;
}
.step-container {
    display: flex;
    width: 22%;
    margin: 1%;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: flex-start;
    justify-content: stretch;
}
.number {
    color: #36E9A0;
    font-family: "assistant-extraBold";
    font-size: 7.5vw;
}
.step {
    text-align: start;
    font-size: 2.25vw;
    border-right: #36E9A0 solid 1vh;
    height: 100%;
    padding-right: 5%;
}
@media (max-width: 600px) {
.steps-container {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: stretch;
    margin: 0 auto;
    /* margin-top: 5vh; */
    width: 80%;
    gap: 4vw; /* spacing between step-containers */
}

.step-container {
    display: grid;
    grid-template-columns: 20% 1fr;
    align-items: stretch;
    width: 100%;
}

.number {
    font-size: 20vw;
    display: flex;
    align-items: center;
    justify-content: center;
}

.step {
    font-size: 6vw;
    padding-right: 6%;
    border-right: #36E9A0 solid 0.75vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    /* min-height: 30vw; */
}
}

</style>
