<template>
  <div class="screen">
    <h1 >✨ Congratulations ✨</h1>
    <h3 >{{ Math.round(timer/1000) }} seconds</h3>
    <button @click="onStart">Start Again</button>
  </div>
</template>


<script>
export default {
    props: {
        timer:{
            type:Number,
            required:true
        }
    },
    methods: {
        onStart() {
            this.$emit("startAgain")
        }
    }
}
</script>

<style lang="css">

</style>