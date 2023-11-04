<template>
  <div class="counter" :class="{ change: change }">
    <div class="counter-back">
      <div class="counter-top">
        <div class="number">{{ back }}</div>
      </div>
      <div class="counter-bottom">
        <div class="number">{{ back }}</div>
      </div>
    </div>
    <div class="counter-front" @animationend="switchEnd">
      <div class="counter-top">
        <div class="number">{{ front }}</div>
      </div>
      <div class="counter-bottom">
        <div class="number">{{ front }}</div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
export default {
  name: 'Counter',
  props: {
    number: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      front: this.number,
      back: 4,
      change: false,
    }
  },
  watch: {
    number(current, prev) {
      this.front = prev
      this.back = current
      this.change = true
    },
  },
  methods: {
    switchEnd() {
      this.change = false
      this.front = this.number
      this.back = 0
    },
  },
}
</script>

<style lang="scss" scoped>
$width: 150px;
$height: 175px;
$hole: 5px;

.counter {
  width: $width;
  height: $height;
  position: relative;
}
.counter-back {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9998;
  animation: flip-back-index 0.5s forwards;
  .counter-bottom {
    transform: rotateX(180deg);
    transform-origin: top;
  }
}
.counter-front {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  .counter-top {
    transform: rotateX(0deg);
    transform-origin: bottom;
  }
}

.change {
  .counter-front {
    animation: flip-front-index 0.5s forwards;
    .counter-top {
      animation: flip-front 0.5s forwards;
    }
  }
  .counter-back {
    animation: flip-back-index 0.5s forwards;
    .counter-bottom {
      animation: flip-back 0.5s forwards;
    }
  }
}
.counter-top {
  height: 50%;
  width: 100%;
  overflow: hidden;
  background-color: hsl(236, 21%, 26%);
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  background: radial-gradient(
      circle at 0 100%,
      rgba(204, 0, 0, 0) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 100% 100%,
      rgba(204, 0, 0, 0) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 100% 0,
      hsl(236, 21%, 26%) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 0 0,
      hsl(236, 21%, 26%) $hole,
      hsl(236, 21%, 26%) $hole + 1
    );
  background-position: bottom left, bottom right, top right, top left;
  background-size: 50% 50%;
  background-repeat: no-repeat;
}
.counter-bottom {
  height: 50%;
  width: 100%;
  overflow: hidden;
  background-color: hsl(236, 21%, 26%);
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
  background: radial-gradient(
      circle at 0 100%,
      hsl(236, 21%, 26%) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 100% 100%,
      hsl(236, 21%, 26%) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 100% 0,
      rgba(204, 0, 0, 0) $hole,
      hsl(236, 21%, 26%) $hole + 1
    ),
    radial-gradient(
      circle at 0 0,
      rgba(204, 0, 0, 0) $hole,
      hsl(236, 21%, 26%) $hole + 1
    );
  background-position: bottom left, bottom right, top right, top left;
  background-size: 50% 50%;
  background-repeat: no-repeat;
  filter: brightness(1.1);
  .number {
    transform: translateY(-50%);
  }
}

.number {
  height: $height;
  width: 100%;
  display: flex;
  font-family: 'Red Hat Text', sans-serif;
  font-weight: 700;
  font-size: 86px;
  color: hsl(345, 95%, 68%);
  align-content: center;
  align-items: center;
  justify-content: center;
  text-align: center;
}

@media screen and (max-width: 786px) {
  $width: 75px;
  $height: 60px;
  $hole: 5px;

  .counter {
    width: $width;
    height: $height;
  }

  .counter-top {
    background: radial-gradient(
        circle at 0 100%,
        rgba(204, 0, 0, 0) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 100% 100%,
        rgba(204, 0, 0, 0) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 100% 0,
        hsl(236, 21%, 26%) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 0 0,
        hsl(236, 21%, 26%) $hole,
        hsl(236, 21%, 26%) $hole + 1
      );
  }
  .counter-bottom {
    background: radial-gradient(
        circle at 0 100%,
        hsl(236, 21%, 26%) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 100% 100%,
        hsl(236, 21%, 26%) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 100% 0,
        rgba(204, 0, 0, 0) $hole,
        hsl(236, 21%, 26%) $hole + 1
      ),
      radial-gradient(
        circle at 0 0,
        rgba(204, 0, 0, 0) $hole,
        hsl(236, 21%, 26%) $hole + 1
      );
  }

  .number {
    height: $height;
    font-size: 36px;
  }
}
@keyframes flip-back-index {
  0% {
    z-index: 9998;
  }
  50% {
    z-index: 9999;
  }
  100% {
    z-index: 9999;
  }
}
@keyframes flip-front-index {
  0% {
    z-index: 9999;
  }
  50% {
    z-index: 9998;
  }
  100% {
    z-index: 9998;
  }
}

@keyframes flip-back {
  from {
    transform: rotateX(180deg);
  }
  to {
    transform: rotateX(0deg);
  }
}
@keyframes flip-front {
  from {
    transform: rotateX(0deg);
  }
  to {
    transform: rotateX(180deg);
  }
}
</style>
