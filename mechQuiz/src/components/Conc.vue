
<template>
    <div id="conc-page">
        <div id="conc-text">You got {{ percent }}%!<br/>
        <button class="btn btn-light" @click="reload()">Reset</button>
        </div>
    </div>
</template>

<script>
    export default{
        props: {
            correct: Number,
            incorrect: Number
        },
        data(){
            return{
                percent: 0
            }
        },
        created(){
            this.percent = Math.round(100 * this.correct / (this.correct + this.incorrect))
            console.log(this.correct)
            console.log(this.incorrect)
        },
        methods: {
            reload(){
                window.location.reload()
            }
        }
    }
</script>

<style>
    #conc-page{
        position: absolute;
        height: 100vh;
        width: 100%;
        background-color: rgb(39, 39, 39);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    #conc-text{
        color: white;
        font-size: 40px;
        text-align: center;
    }
</style>