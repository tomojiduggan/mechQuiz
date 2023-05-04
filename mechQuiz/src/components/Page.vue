<script>
import Intro from "./Intro.vue"
import Quiz from "./Quiz.vue"
import Conc from "./Conc.vue"

export default{
    data(){
        return{
            count: 4,
            started: false,
            countClass: "",
            finished: false,
            correct: 0,
            incorrect: 0
        }
    },
    props: {
    },
    components: {
        Intro, Quiz, Conc
    },
    methods: {
        countDownTimer () {
            this.countClass = "animated"
            if (this.count > 0) {
                setTimeout(() => {
                    this.count -= 1
                    this.countDownTimer()
                }, 1000)
            }
            if (this.count == 0){
                this.started = true
            }
            
        },
        conclude(payload){
            this.correct = payload["correct"]
            this.incorrect = payload["incorrect"]
            this.finished = true
        }
    },

}
</script>

<template>
    <Intro @startQuiz="this.countDownTimer()" v-if="!started"></Intro>
    <Quiz v-if="started && !finished" @finish="conclude"></Quiz>
    <Conc v-if="finished" :correct="correct" :incorrect="incorrect"></Conc>

    <div v-if="count!=4 && count!=0" id="countdown" :class="countClass">{{ count }} </div>
</template>


<style>
@font-face{font-family: talk-comic; src: url('./fonts/Talk Comic.otf')}
    #countdown{
        color: white;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
        width: 100%;
        height: 30%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 100px;
        font-family: talk-comic;
    }

    @keyframes example {
  0%   {background-color: rgb(255, 232, 183);}
  100% {background-color: rgb(224, 141, 64);}
}

    .animated{
        animation-name: example !important;
        animation-duration: 1s !important;

        animation-iteration-count: infinite !important;
        color: white !important;
        background-color: red;

    }



</style>