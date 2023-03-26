<template>
  <div class="time-widget"
  :class="isActive ? 'active' : 'disactive'"
  >
    <div class="time-widget_value">
      <p class="hours"
      v-if="hours > 0"
      >
       {{hours > 9 ? hours + ':' : '0' + hours + ':'}}
      </p>

      <p class="minutes"
      v-if="hours > 0 ? minutes >= 0 :  minutes > 0"
      >
       {{minutes > 9 ? `${minutes}:` : `0${minutes}:`}}
      </p>

      <p class="seconds">
       {{getSeconds}}
      </p>
    </div>

    <div class="time-widget_option">
      <div class="option_play"
      v-if="!isActive"
      @click="isActive = true"
      >
      </div>

      <div class="option_pause" 
      v-else
      @click="isActive = false"
      >
      <div></div>
      <div></div>
      </div>

      <div class="option_stop"
      @click="clearTime"
      >
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    name: 'time-widget',

    props: {
      timeSet: Array
    },

    data() {
      return {
        isActive: false,
        seconds:0,
        minutes: 0,
        hours: 0,
        interval: null,
      }
    },

    methods: {
      clearTime() {
        this.isActive = false
        this.seconds = 0
        this.minutes = 0
        this.hours = 0
      }
    },

    computed: {
      getSeconds() {
        if (this.hours === 0 && this.minutes === 0) {
          if (this.seconds === 0) {
            return this.seconds;
          } else {
            if (this.seconds > 9) {
              return this.seconds
            } else {
              return `0${this.seconds}`
            }
          }
        } else {
          if (this.seconds > 9) {
            return this.seconds;
          } else {
            return `0${this.seconds}`
          }
        }
      }
    },

    watch: {
      isActive() {
        if (this.isActive === true) {
          this.interval = setInterval((() => {
            this.seconds += 1
          }), 1000)
        } else {
          clearInterval(this.interval)
        }
      },

      minutes() {
        if (this.minutes === 60) {
          this.minutes = 0
          this.hours += 1
        }
      },

      seconds() {
        if (this.seconds === 60) {
          this.seconds = 0
          this.minutes += 1
        }
      }
    },

     mounted() {
      if (this.timeSet) {
        this.hours = this.timeSet[0]
        this.minutes = this.timeSet[1]
        this.seconds = this.timeSet[2]
      }
  }

  }

</script>

<style lang="scss" scoped>

.time-widget {
  height: 120px;
  width: 255px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
  background: #696969;
}

.time-widget_value {
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.time-widget_option {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60px;
  .option_play, .option_stop {
    width: 20px;
    height: 20px;
    border-radius: 2px;
    cursor: pointer;
  }
  .option_pause {
    height: 20px;
    width: 10px;
  }
}

.option_pause {
  display: flex;
  justify-content: space-between;
  cursor: pointer;
  div {
    width: 3px;
    height: 20px;
  }
}

.option_play {
   clip-path: polygon(100% 50%, 0 100%, 0 0);
}

.option_stop {
  margin-left: 50px;
}

.disactive {
  .time-widget_value {
    border-bottom: 1px solid #9E9E9E;
    color: #9E9E9E;
  }
  .time-widget_option {
    .option_play, .option_stop {
      background: #9E9E9E;
      &:hover {
          background: #FFFFFF;
        }
    }
    .option_pause {
      div {
        background: #9E9E9E;
      }
      &:hover {
        div {
          background: #FFFFFF;
        }
      }
    }
  }
}

.active {
  .time-widget_value {
    border-bottom: 1px solid #FFFFFF;
    color: #FFFFFF;
  }

  .time-widget_option {
    .option_play, .option_stop {
      background: #FFFFFF;
      &:hover {
          background: #9E9E9E;
        }
    }
    .option_pause {
      div {
        background: #FFFFFF;
      }
      &:hover {
        div {
          background: #9E9E9E;
        }
      }
    }
  }
}


</style>