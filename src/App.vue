<template>
  <h1>Hello game</h1>
  <MainScreen v-if="status === 'default'" @onStart="onHandleStart($event)"></MainScreen>
  <ResultScreen v-if="status === 'result'" :timer="timer" @startAgain="onStartAgain"></ResultScreen>
  <InteractScreen v-if="status === 'match'" :cardsContext="settings.cardsContext" @onFinish="onResult"></InteractScreen>

  <!-- <CardPokemon></CardPokemon> -->
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";

import {shuffled} from "../utils/array"
export default {
  name: "App",
  data() {
    return {
      settings:{
        totalBlocks:0,
        cardsContext:[],
        timeStart:null
      },
      status: "default",
      timer:0
    };
  },
  components: {
    MainScreen,
    ResultScreen,
    InteractScreen,

  },
  methods: {
    onHandleStart(config) {
      console.log("running handle start",config)
      this.settings.totalBlocks = config.num;

      const firstCards = Array.from(
        {length:this.settings.totalBlocks/2},(_,i) => i+1
        )

        const secondCards = [...firstCards]

        const cards = [...firstCards,...secondCards]

        this.settings.cardsContext = shuffled(shuffled(shuffled(cards)))
        this.settings.timeStart=new Date().getTime()

      console.log(this.settings.cardsContext )
      this.status = "match"
    },
    onResult() {
      this.timer = new Date().getTime() - this.settings.timeStart
      this.status = "result"
    },
    onStartAgain() {
      this.status = "default"
    }
  }
};
</script>

<style></style>
