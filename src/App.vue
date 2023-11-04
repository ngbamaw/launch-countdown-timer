<template>
  <div id="app">
    <p class="header-text">We're launching soon</p>
    <div class="full-counter">
      <div v-for="(counter, index) in time" :key="timeLabels[index]">
        <Counter :number="counter" />
        <p class="label-time">{{ timeLabels[index] }}</p>
      </div>
    </div>
    <div class="share-btn">
      <button></button>
      <button></button>
      <button></button>
    </div>
  </div>
</template>

<script lang="ts">
import moment from 'moment'
import Counter from './components/Counter.vue'
import { defineComponent } from 'vue'

const end = moment().add(13, 'days')

export default defineComponent({
  name: 'App',
  components: {
    Counter,
  },
  data() {
    return {
      number: 10,
      time: this.getRemainTime(),
      timeLabels: ['DAYS', 'HOURS', 'MINUTES', 'SECONDS'],
      interval: undefined as number | undefined,
    }
  },
  mounted() {
    this.interval = setInterval(() => (this.time = this.getRemainTime()), 1000)
  },
  beforeDestroy() {
    clearInterval(this.interval)
  },
  methods: {
    getRemainTime() {
      const start = moment()
      const diff = end.diff(start)

      const f = moment.utc(diff).format('DDD:HH:mm:ss')
      return f.split(':').map(Number)
    },
  },
})
</script>

<style lang="scss">
#app {
  height: 100vh;
  display: flex;
  flex-direction: column;
  background: url('./assets/images/pattern-hills.svg'),
    url('./assets/images/bg-stars.svg'), hsl(235, 16%, 14%);
  background-repeat: no-repeat;
  background-position: bottom, center;
  background-size: 100%, cover;
  font-family: 'Red Hat Text', sans-serif;
  font-weight: 700;
  letter-spacing: 3px;
  overflow: hidden;
}
.full-counter {
  margin: auto;
  margin-top: 0;
  display: flex;
  gap: 48px;
}

.header-text {
  text-transform: uppercase;
  color: white;
  margin: 20vh auto;
  margin-bottom: 10vh;
  font-size: 24px;
  text-align: center;
}
.label-time {
  color: hsl(237, 18%, 59%);
  font-family: 500;
  text-align: center;
  margin-top: 36px;
}
.share-btn {
  margin: 5vw auto;
  button {
    height: 50px;
    width: 50px;
    transition: all 0.2s;
    background-color: hsl(237, 18%, 59%);
    &:hover {
      background-color: hsl(345, 95%, 68%);
    }
    &:nth-of-type(1) {
      mask: url('./assets/images/icon-facebook.svg') center no-repeat;
    }
    &:nth-of-type(2) {
      mask: url('./assets/images/icon-pinterest.svg') center no-repeat;
    }
    &:nth-of-type(3) {
      mask: url('./assets/images/icon-instagram.svg') center no-repeat;
    }
  }
}

@media screen and (max-width: 786px) {
  #app {
    background-size: auto 30%, cover;
    background-position: bottom right -200px, center;
  }
  .header-text {
    width: 80%;
  }
  .full-counter {
    gap: 12px;
  }
  .label-time {
    font-size: 8px;
    margin-top: 16px;
  }
  .share-btn {
    margin: 10vw auto;
  }
}
</style>
