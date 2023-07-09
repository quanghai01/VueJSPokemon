<template>
  <div
    class="card" :class="{disabled:isDisabled}"
    style="height: 198px; width: 148.5px; perspective: 297px"
    @click="onRotate"
  >
    <div class="card__inner" :class="{ 'is-flipped': isRote }">
      <div class="card__face card__face--front">
        <div class="card__content" style="background-size: 49.5px 49.5px"></div>
      </div>
      <div class="card__face card__face--back">
        <div class="card__content" :style="{
            backgroundImage:`url(${require('@/assets/' + imgBackFaceUrl)})`
        }"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRote: false,
      isDisabled:false
    };
  },
  props:{
    card:{
        type:[String,Number,Array,Object],
    },
    imgBackFaceUrl:{
        type:String,
        required:true
    }
  },
  methods: {
    onRotate() {
        if(this.isDisabled) return false
      this.isRote = !this.isRote;
      if(this.isRote)  this.$emit("onFlip",this.card)
    },

    onFlipBack() {
        this.isRote = false
    },
    onFlipDisabled() {
        this.isDisabled=true
    }
  },
};
</script>

<style lang="css">
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}
.card.disabled .card__inner{
    cursor: auto;

}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background: url(../assets/images/icon_back.png) no-repeat 50%;
  height: 100%;
  width: 100%;
}
.card__face--back {
  /* background-color: #f3f3f3; */
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
}

.card__content {

    display: flex;
    align-items: center;
    width: 100%;
    height: 100%;
    background-size: contain;
    background-repeat: no-repeat;
}
</style>
