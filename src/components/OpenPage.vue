<template>
    <div id="open-page">
        <img src="@/assets/media/bg.jpg" alt="bg" class="bg-pic">
        <div class="ombre"></div>
        <div id="title">המענה הרפואי ופלגת הפינוי</div>
        <div class="button" @click="nextPage">שנתחיל?</div>
    </div>
</template>

<script>
    export default {
        name: "open-page",
        methods: {
            nextPage() {
                this.$emit('next-page');
            }
        }
    }
</script>

<style scoped>
#open-page {
    height: 100vh;
    overflow: hidden;
    width: 100vw;
    background-color: white;
}
.bg-pic {
    position: absolute;
    top: 0;
    right: 0;
    height: 100vh;
    width: 75vw;
    object-fit: cover;
    z-index: 1;
}
.ombre {
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 0;
    z-index:2;
    right: 0;
    background: linear-gradient(90deg, #1F1E23, #202C2F, #202C2F, #202c2fd8, #202c2f63, #202c2f0d);
}
#title {
    font-family: "assistant-extraBold";
    width: 30vw;
    margin: auto;
    margin-top: 20vh;
    font-size: 5vw;
    text-shadow: 1px 0px 3px #000000;
    z-index: 3;
    position: relative;
}
.button {
    background-color: white;
    width: fit-content;
    padding: 1%;
    cursor: pointer;
    border-radius: 2vh;
    font-size: 2vw;
    margin: auto;
    margin-top: 4vh;
    font-family: "assistant-extraBold";
    box-shadow: rgba(0, 0, 0, 0.5) 1vw 1vh 2vw;
    z-index: 3;
    position: relative;
    color: #1F1E23;
    transition: all 0.4s;
}
.button:hover {
    transform: scale(0.9);
}
@media (max-width: 600px) {
    #title {
        margin-top: 25vh;
        width: 80vw;
        font-size: 13vw;
    }
    .ombre {
        background: linear-gradient(180deg, #1F1E23,#1F1E23 , #202C2F, #202C2F, #202c2fd8, #202c2f63, #202c2f0d);
    }
    .bg-pic {
        bottom: 0;
        right: 0;
        top: unset;
        height: 65vh;
        width: 100vw;
        z-index: 1;
    }
    .button {
        padding: 1.2%;
        border-radius: 1vh;
        font-size: 7vw;
        margin-top: 4vh;
        box-shadow: rgba(0, 0, 0, 0.5) 1vw 0.5vh 1vw;
    }
}
</style>