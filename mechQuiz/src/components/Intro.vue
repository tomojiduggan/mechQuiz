
<template>
    <div id="page">
        <div id="intro-text">
            <h1 id="title" class="fw-bold">Welcome to a multiple-choice mechanics quiz app!</h1>
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
        background-color: black;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    #title{
        margin-bottom: 2rem;
    }
    #intro-text{
        color: white;
        text-align: center;
    }
</style>