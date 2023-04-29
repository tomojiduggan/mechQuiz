<script>
import Intro from "./Intro.vue"
import Quiz from "./Quiz.vue"

export default{
    data(){
        return{
            count: 6,
            started: false,
            countClass: ""
        }
    },
    props: {
    },
    components: {
        Intro, Quiz
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
            
        }
    },

}
</script>

<template>
    <Intro @startQuiz="this.countDownTimer()" v-if="!started"></Intro>
    <Quiz v-if="started"></Quiz>

    <div v-if="count!=6 && count!=0" id="countdown" :class="countClass">{{ count }} </div>
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
  0%   {background-color: rgb(0, 52, 165);}
  100% {background-color: rgb(64, 147, 224);}
}

    .animated{
        animation-name: example !important;
        animation-duration: 1s !important;

        animation-iteration-count: infinite !important;
        color: white !important;
        background-color: red;

    }



</style>