<template>
  <div class="screen">
    <h1 class="title-game">POKE MEMORIES</h1>
    <p>Select mode to start game</p>

    <div class="modes">
      <button @click="onClick(4)">
        <span>2X2</span>
        <span>Easy</span>
      </button>
      <button @click="onClick(16)">
        <span>4X4</span>
        <span>Normal</span>
      </button>
      <button @click="onClick(36)">
        <span>6X6</span>
        <span>Hard</span>
      </button>
      <button @click="onClick(64)">
        <span>8X8</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {

  methods: {
    onClick(num) {
      this.$emit("onStart",{num})
    }
  }
};
</script>

<style lang="css">

.screen {
    width: 100%;
    height: auto;

    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: #212121;
    color: #f3f3f3;
}

.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}
.screen p {
  font-size: 2rem;
}
.modes {
  display: flex;
  margin-top: 2rem;
}

.modes button {
  font: #fff;
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid #f3f3f3;
  color: #f3f3f3;
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}
.modes button:hover {
    background-color: #f3f3f3;
    color: #212121;
}
.modes button span:first-child {
  font-size: 2rem;
}
.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
</style>
