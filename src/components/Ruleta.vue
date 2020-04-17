<template>
  <div class="container">
    <div class="circle">
      <div
        class="arrow"
        :style="{ transform: 'rotate(' + rotationArrow + 'deg)' }"
      />
      <span class="op1" v-text="option1" />
      <span class="op2" v-text="option2" />
      <span class="op3" v-text="option3" />
      <span class="op4" v-text="option4" />
    </div>

    <button v-if="!isInit" class="btn" @click="rotateArrow">Girar</button>
  </div>
</template>

<script>
export default {
  name: "Ruleta",
  data() {
    return {
      isInit: false,
      rotationArrow: 90,
      velocityArrow: 1,
      option1: "Tirarse por un puente",
      option2: "Dar un milllón a alguien",
      option3: "No comer durante 1 día",
      option4: "No ver la TV durante 1 semana",
    };
  },
  methods: {
    rotateArrow() {
      this.isInit = true;
      let luck = this.getRandomArbitrary(5, 10) * 1000;
      console.log(luck);

      const time = setInterval(() => {
        this.rotationArrow++;
      }, this.velocityArrow);

      setTimeout(() => {
        clearInterval(time);
        this.isInit = false;
      }, 3000 + luck);
    },

    getRandomArbitrary(min, max) {
      return Math.random() * (max - min) + min;
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  .circle {
    width: 30rem;
    height: 30rem;
    background: linear-gradient(45deg, blue, blue 100%),
      linear-gradient(135deg, green, green),
      linear-gradient(225deg, yellow, yellow), linear-gradient(315deg, red, red);
    background-size: 50% 50%;
    background-position: 0% 0%, 0% 100%, 100% 0%, 100% 100%;
    background-repeat: no-repeat;
    border-radius: 50%;
    position: relative;
    .arrow {
      width: 15rem;
      height: 1rem;
      background: purple;
      border-radius: 2rem;
      position: absolute;
      top: 48%;
      right: 45%;
      transform-origin: 90% 50%;
      z-index: 9;
    }
    .op1 {
      background: rgb(69, 69, 251);
      color: whitesmoke;
      border-radius: 1rem;
      position: absolute;
      padding: 0.5rem;
      top: 15%;
      left: 15%;
      width: 25%;
      height: 10%;
    }
    .op2 {
      background: rgb(255, 255, 133);
      border-radius: 2rem;
      position: absolute;
      padding: 0.5rem;
      top: 15%;
      right: 15%;
      width: 25%;
      height: 10%;
    }
    .op3 {
      background: rgb(45, 133, 45);
      color: whitesmoke;
      border-radius: 2rem;
      position: absolute;
      padding: 0.5rem;
      bottom: 15%;
      left: 15%;
      width: 25%;
      height: 10%;
    }
    .op4 {
      background: rgb(251, 54, 54);
      border-radius: 2rem;
      position: absolute;
      padding: 0.5rem;
      bottom: 15%;
      right: 15%;
      width: 25%;
      height: 10%;
    }
  }
  .btn {
    position: absolute;
    bottom: -25%;
    width: 10rem;
    height: 5rem;
    border-radius: 2rem;
  }
}
</style>
