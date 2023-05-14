
<template>
    <div id="quizPage" :class="color">
        <div id="count-contain">
            <div class="countdown" v-if="!answered">
                <span id="count-text">Time left: {{ timeLeft }}</span>
            </div>

            <div class="counter">
                <span>Correct: {{ right }}</span><br/>
                <span>Incorrect: {{ wrong }}</span>
            </div>
        </div>

        <div class="container">
            <div>
                <p class="question-text" v-html="question"></p>
            </div>
            <div class="choices list-group">
                <Choice v-on:answered="submit" v-for="(answer, index) in answers" :correct="index==correct" :text=answer :order=index :clickable="!answered"></Choice>
            </div>

            <div class="d-grid" v-if="answered">
                <button @click="swap" class="btn btn-outline-light">Proceed</button>
                <h1>{{ display() }}</h1>
            </div>
            
            <div class="progress" role="progressbar" aria-label="Animated striped example" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">
                <div class="progress-bar progress-bar-striped progress-bar-animated bg-info" :style="{width: progress + '%'}"></div>
            </div>
        </div>

        
    </div>
</template>

<script>
import Choice from "./Choice.vue"
import qArray from "./data.json"


function shuffle(array) {
  let currentIndex = array.length,  randomIndex;

  // While there remain elements to shuffle.
  while (currentIndex != 0) {

    // Pick a remaining element.
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [array[currentIndex], array[randomIndex]] = [
      array[randomIndex], array[currentIndex]];
  }

  return array;
}


export default{
    created(){
        console.log("Quiz Loaded.")
        this.qOrder = shuffle(qArray)
        this.question = this.qOrder[0]["question"] //First question asked
        console.log(this.question)
        this.answers = this.qOrder[0]["answers"] //Answers Displayed
        this.correct = this.qOrder[0]["correct"] //Correct answer, in index of array
        this.timeLeft = this.qOrder[0]["time"] //set amount of time user has to answer question

        this.countDownTimer()
    },
    components: {
        Choice
    },
    data(){
        return{
            question: "",
            qOrder: [],
            answers: [],
            correct: 0,
            answered: false,
            qNum: 0,
            right: 0,
            wrong: 0,
            color: "",
            valid: false,
            timeLeft: 0,
            progress: 0
        }
    },
    methods: {
        submit(i){
            console.log(i)
            if(this.correct==i){
                console.log("Correct!")
                this.right += 1
                this.color = "green"
                this.valid = true
            }
            else{
                console.log("Wrong! It was " + String(this.correct))
                this.wrong += 1
                this.color = "red"
                this.valid = false
            }
            this.answered = true
        },
        swap(){
            console.log(this.qNum)
            console.log(this.qOrder.length)
            if(!(this.qNum == this.qOrder.length-1)){
                console.log("swap!")
                this.qNum += 1
                this.question = this.qOrder[this.qNum]["question"]
                this.answers = this.qOrder[this.qNum]["answers"]
                this.correct = this.qOrder[this.qNum]["correct"]
                this.timeLeft = this.qOrder[this.qNum]["time"]
                this.progress = (this.qNum) * 100 / this.qOrder.length

                this.answered = false
                this.color = ""
                
                this.countDownTimer()
            } else {
                this.$emit("finish", {"correct": this.right, "incorrect": this.wrong})
            }
        },
        display(){
            if(this.valid){
                return("That is correct!")
            }
            else{
                return("Incorrect!")
            }
        },
        countDownTimer () {
            if(!this.answered){
                if (this.timeLeft > 0) {
                    setTimeout(() => {
                        this.timeLeft -= 1
                        this.countDownTimer()
                    }, 1000)
                }
                if (this.timeLeft == 0){
                    this.submit(-1)
                }
            }
            
        }
    }
    
}
</script>

<style>

    #quizPage{
        height: 100vh;
        width: 100%;
        background-color: rgb(37, 37, 37);
        display: flex;
        justify-content: center;
        color: white;
        transition-duration: 0.2s;
    }
    
    .red{
        background-color: rgb(65, 30, 30) !important;
    }
    .green{
        background-color: rgb(44, 87, 44) !important;
    }

    #count-contain{
        position: absolute;
        width: 100vw;
        height: 10vh;
        top: 0;
        
    }
    .countdown{
        position: relative;
        width: 50%;
        padding: 2rem
    }
    @keyframes counts{
        from {color: white;}
        to {color: red;}
    }
    #count-text{
        font-size: 50px;
        animation-name: counts;
        animation-duration: 1s;
        animation-timing-function: ease;
        animation-iteration-count: infinite;
    }


    .counter{
        position: absolute;
        padding: 2rem;
        right: 0;
        top: 0;
    }

    .container{
        position: relative;
        margin-top: 14vh;
    }
    .question-text{
        text-align: center;
        font-size: 30px;
    }
    .choices{
        margin-bottom: 1rem;
    }
    h1{margin-bottom: 2rem;}
    .d-grid{
        text-align: center;
    }
    .btn-outline-light{
        margin-bottom: 1.5rem;
    }

    #progress{
        position: absolute;
        bottom: 0;

    }


</style>