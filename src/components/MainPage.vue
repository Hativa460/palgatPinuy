<template>
    <div id="main-page">
        <div id="hamburger-menu" @click="showNav" v-if="openNav===false">
            <div class="bar"></div>
            <div class="bar"></div>
            <div class="bar"></div>
        </div>
        <nav-bar :rank="rank" v-if="openNav" :topicNum="topicNum" @close-menu="showNav" @switchPage="switchPage"></nav-bar>
        <div v-if="rank === 'mm'">
            <fight-data v-if="topicNum === 0" @next-page="nextPage"></fight-data>
            <pointers v-if="topicNum === 1" @next-page="nextPage"></pointers>
            <demonstrations v-if="topicNum === 2" @next-page="nextPage"></demonstrations>
            <commandors :rank="rank" v-if="topicNum === 3" @next-page="nextPage"></commandors>
            <reports v-if="topicNum === 4" @next-page="finalMain"></reports>
        </div>
        <div v-if="rank === 'mp'">
            <treatment-ability v-if="topicNum === 0" @next-page="nextPage"></treatment-ability>
            <fight-data v-if="topicNum === 1" @next-page="nextPage"></fight-data>
            <pointers v-if="topicNum === 2" @next-page="nextPage"></pointers>
            <demonstrations v-if="topicNum === 3" @next-page="nextPage"></demonstrations>
            <event-steps v-if="topicNum === 4" @next-page="nextPage"></event-steps>
            <independence v-if="topicNum === 5" @next-page="nextPage" :rank="rank"></independence>
            <commandors :rank="rank" v-if="topicNum === 6" @next-page="nextPage"></commandors>
            <reports v-if="topicNum === 7" @next-page="finalMain"></reports>
        </div>
        <div v-if="rank === 'mgd'">
            <treatment-ability v-if="topicNum === 0" @next-page="nextPage"></treatment-ability>
            <fight-data v-if="topicNum === 1" @next-page="nextPage"></fight-data>
            <pointers v-if="topicNum === 2" @next-page="nextPage"></pointers>
            <demonstrations v-if="topicNum === 3" @next-page="nextPage"></demonstrations>
            <event-steps v-if="topicNum === 4" @next-page="nextPage"></event-steps>
            <independence v-if="topicNum === 5" @next-page="nextPage" :rank="rank"></independence>
            <commandors :rank="rank" v-if="topicNum === 6" @next-page="nextPage"></commandors>
            <reports v-if="topicNum === 7" @next-page="finalMain"></reports>
        </div>
    </div>
</template>

<script>
import NavBar from "@/components/NavBar";
import TreatmentAbility from "@/components/TreatmentAbility";
import FightData from "@/components/FightData";
import Pointers from "@/components/Pointers";
import Demonstrations from "@/components/Demonstrations";
import EventSteps from "@/components/EventSteps";
import Independence from "@/components/Independence";
import Commandors from "@/components/Commandors";
import Reports from "@/components/Reports";

export default {
    name: "main-page",
    props: ["rank"],
    components: {
        NavBar,
        TreatmentAbility,
        FightData,
        Pointers,
        Demonstrations,
        EventSteps,
        Independence,
        Commandors,
        Reports
    },
    data() {
        return {
            openNav: false,
            topicNum: 0
        }
    },
    methods: {
        showNav() {
            this.openNav = !this.openNav;
        },
        switchPage(index) {
            this.topicNum = index;
            this.openNav = !this.openNav;
        },
        nextPage() {
            this.topicNum ++;
        },
        finalMain() {
            this.$emit('next-page');
        }

    }
}
</script>

<style scoped>
#main-page {
    height: 100%;
    overflow-x: hidden;
    width: 100vw;
}
#hamburger-menu {
    position: fixed;
    top: 2%;
    left: 1%;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
    z-index: 3;
    cursor: pointer;
}
.bar {
    background: white;
    border-radius: 0.25vw;
    height: 2vh;
    width: 5vw;
    margin: 5%;
}
@media (max-width: 600px) {
    #hamburger-menu {
        left: 2%;
    }
    .bar {
        height: 1vh;
        width: 12vw;
        border-radius: 0.5vw;
    }
}
</style>