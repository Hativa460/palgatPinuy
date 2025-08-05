<template>
    <div id="independence">
        <div class="title">{{ title }}</div>
        <div class="list-container">
            <div v-for="(item, index) in list" :key="index" class="txt">{{index+1}}. {{item}}</div>
        </div>
        <div class="next-btn" @click="nextPage">מושלם הבנתי</div>
    </div>
</template>

<script>
    import json from "../../text.json";
    export default {
        name: "independence",
        props: ["rank"],
        data() {
            return {
                title: json["independence"][this.rank]["title"],
                list: json["independence"][this.rank]["list"]
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
    #indepndence {
        height: 100vh;
        width: 100vw;
        overflow-x: hidden; /* only hide horizontal, not vertical */
        overflow-y: visible;
    }
    .list-container {
        border-radius: 2vw;
        padding: 3%;
        padding-top: 7vh;
        width: 55vw;
        margin: auto;
        margin-top: -3vh;
        border: solid 1vh #36E9A0;
        box-shadow: #36E9A0 0px 8px 20px -4px;
        /* box-shadow: #36E9A0 0px 50px 100px -20px, #36E9A0 0px 30px 60px -30px; */
        border-top: none;
    }
    .txt {
        margin: auto;
        text-align: start;
        width: 50vw;
        font-size: 2.25vw;
        margin-top: 1vh;
        margin-bottom: 1vh;
    } 
    @media (max-width: 600px) {
        .list-container {
            border-radius: 2vh;
            padding: 3%;
            padding-top: 7vh;
            width: 85vw;
            margin: auto;
            margin-top: -3vh;
            border: solid 1vh #36E9A0;
            box-shadow: #36E9A0 0px 8px 20px -4px;
            border-top: none;
        }
        .txt {
            margin: auto;
            text-align: start;
            width: 70vw;
            font-size: 4.75vw;
            margin-top: 1vh;
            margin-bottom: 1vh;
        } 
    }

</style>