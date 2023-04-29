
<template>
    <div class="card">
        <div class="card-body">
            {{ text }}
        </div>
        <button @click="emitStart" type="button" class="btn btn-outline-light btn-lg">Proceed</button>

    </div>
</template>

<script>
export default{
    props: {
        text: String
    },

}
</script>

<style>

</style>