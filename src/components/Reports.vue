<template>
    <div id="reports">
        <div class="title">{{ title }}</div>
        <div class="list-container">
            <div class="item-container" v-for="(item, index) in list" :key="index">
                <img src="@/assets/media/check.svg" alt="pic" class="check">
                <div class="txt">{{item}}</div>
            </div>
        </div>
        <div class="next-btn" @click="nextPage">כןכן אני יודע</div>
    </div>
</template>

<script>
    import json from "../../text.json";
    export default {
        name: "reports",
        data() {
        return {
            title: json["reports"]["title"],
            list: json["reports"].list
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
#reports {
  height: 100vh;
  overflow: hidden;
  width: 100vw;
}
.list-container {
    /* margin: auto;
    margin-top: 3vh; */
    position: absolute;
    top: 50%;
    right: 50%;
    transform: translate(50%, -50%);
    display: flex;
    flex-direction: column;
    align-items: center;
}
.item-container {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    margin-top: 1.5vh;
    margin-bottom: 1.5vh;
    /* background-color: aqua; */
    align-items: center;
    width: 35vw;
    justify-content: flex-start;
}
.check {
    height: 8vh;
    max-width: 100%;
    margin-left: 1.25vw;
}
.txt {
    text-align: start;
    font-size: 2.75vw;
}
@media (max-width: 600px) {
    .list-container {
        margin: auto;
        margin-top: 3vh;
        position: relative;
        top: 0%;
        right: 00%;
        transform: none;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .item-container {
        width: 70vw;
    }
    .check {
        height: 4vh;
        max-width: 100%;
        margin-left: 2.5vw;
    }
    .txt {
        text-align: start;
        font-size: 5.5vw;
    }

}
</style>