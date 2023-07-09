<template>
  <div class="screen">
    <h1 class="title-interact">Interact Game Pokemon ...</h1>
    <div class="list-card" :class="`flex-${cardsContext.length}`">
      <CardPokemon
        v-for="(card, index) in cardsContext"
        :key="index"
        
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index: index, value: card }"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>

<script>
import CardPokemon from "./CardPokemon.vue";
export default {
  data() {
    return {
      rules: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardPokemon,
  },
  methods: {
    checkRule(card) {
      if (this.rules.length == 2) return false;

      this.rules.push(card);
      console.log(this.rules);

      if (this.rules.length == 2 && this.rules[0].index != this.rules[1].index) {
        if (
          this.rules.length == 2 &&
          this.rules[0].value == this.rules[1].value
        ) {
          console.log("right...");
          this.$refs[`card-${this.rules[0].index}`][0].onFlipDisabled();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipDisabled();
          this.rules = [];

          const countDisabled = document.querySelectorAll(".screen .card.disabled")
          console.log("countDisabled",countDisabled)

          if(countDisabled && countDisabled.length == this.cardsContext.length - 2) {
            setTimeout(() => {
                this.$emit("onFinish")
            },1000)
          }
        } else if (
          this.rules.length === 2 &&
          this.rules[0].value != this.rules[1].value
        ) {
          console.log("left...");
          setTimeout(() => {
            this.$refs[`card-${this.rules[0].index}`][0].onFlipBack();
            this.$refs[`card-${this.rules[1].index}`][0].onFlipBack();

            this.rules = [];
          }, 1000);
        } else return false;
      } else return false
    },
  },
};
</script>

<style lang="css">
    .flex-4,.flex-16 {
        width: 40%;
    }
    .flex-36,.flex-64 {
        width: 60%;
    }
</style>
