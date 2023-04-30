
<template>
    <div id="page">
        <div id="background-img"></div>
        <div id="intro-text">
            <h1 id="title" class="fw-bold">Welcome to Mech-Rush!</h1>
            <p id="desc">This is a multiple-choice quiz targeting the subject matter of mechanics at <em>Cégep Heritage College</em>.
            As mechanics is one of the harder courses within the science program, many people struggle with stress and time during exams.
            As my teaching tool for my peer tutoring class, I therefore decided to make a quiz with a time limit depending on the complexity of the question.
            This is done to simulate the time limits and pressure present during exams.
            Before you start, make sure you are ready with a paper, pencil and calculator.
        </p>
            <button @click="emitStart" type="button" class="btn btn-outline-light btn-lg">Start!</button>
        </div>
    </div>
</template>

<script>
export default{
    methods: {
        emitStart() {
            this.$emit("startQuiz")
        }
    }
}
</script>

<style>
    #page{
        height: 100vh;
        width: 100%;
        background-color: rgba(0, 0, 0, 0.664);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    #title{
        margin-bottom: 2rem;
    }
    #desc{
        width: 70%;
        margin-left: auto;
        margin-right: auto;
        font-size: 20px;
        margin-bottom: 2rem;
    }
    #intro-text{
        color: white;
        text-align: center;
    }
    #background-img{
        background-image: url("../assets/background.jpg");
        position: absolute;
        height: 100%;
        width: 100%;
        z-index: -1;
    }
</style>