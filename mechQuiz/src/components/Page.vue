<script>
import Intro from "./Intro.vue"
import Quiz from "./Quiz.vue"

export default{
    data(){
        return{
            count: 6
        }
    },
    props: {
        started: false
    },
    components: {
        Intro, Quiz
    },
    watch: {
        start:{
            handler(i){
                while(i != 0){
                    setTimeout(()=>
                        {i -= 1
                        console.log(i)}
                    , 1000)
                }
                started = !started
            }, 
            immediate: true
        }
    },
    computed: {
        
    }
    
}
</script>

<template>
    <Intro @startQuiz="start()" v-if="!started"></Intro>
    <Quiz v-if="started"></Quiz>

    <div v-if="count!=6">{{ count }}</div>
</template>