
<template>
    <div id="quizPage">
        <div class="container">
            <div class="question-text"></div>
        </div>

        
    </div>
</template>

<script>
import Choice from "./Choice.vue"




export default{
    components: {
        Choice
    },
    data(){
        return{
            question: ""
        }
    },
    methods: {
        swap(){
            
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
        align-items: center;
        color: white;
    }


</style>