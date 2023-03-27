<template>
  <div class="time-widget"
  :class="isActive ? 'active' : 'disactive'"
  >
    <div class="time-widget_value">
      <p class="hours"
      v-if="getHours > 0"
      >
       {{getHours > 9 ? getHours + ':' : '0' + getHours + ':'}}
      </p>

      <p class="minutes"
      v-if="getHours > 0 ? getMinutes >= 0 :  getMinutes > 0"
      >
       {{getMinutes > 9 ? `${getMinutes}:` : `0${getMinutes}:`}}
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
      :style="isActive ? 'margin-left: 60px' : ''"
      >
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    name: 'time-widget',

    data() {
      return {
        startPoint: null,
        currentPoint: null,
        stopBefore: null,
        stopAfter: null,
        stopTimePoints: 0,
        resultTime: null,
        isActive: false,
        interval: null
      }
    },

    methods: {
      clearTime() {
        clearInterval(this.interval)
        this.isActive = false
        this.startPoint = null
        this.currentPoint = null
        this.stopAfter = null
        this.stopTimePoints = 0
        this.resultTime = null
        setTimeout(() => {
          this.stopBefore = null
        }, 100);
      }
    },

    computed: {
      getHours() {
      if ((this.resultTime / 3600) !== 0) {
        return Math.floor(this.resultTime / 3600)
      } return 0;
    },

      getMinutes() {
        if ((this.resultTime / 60) !== 0) {
          return Math.floor((this.resultTime - this.getHours * 3600) / 60)
        } return 0;
      },

      getSeconds() {
        const currentSeconds = this.resultTime - (this.getHours * 3600) - (this.getMinutes * 60)
        return currentSeconds;
      },
  },

    watch: {
      isActive() {
        if (this.isActive === true) {
          if (this.startPoint === null) {
            this.startPoint = Date.now()
          }
          if (this.startPoint !== null && this.stopBefore !== null) {
            this.stopAfter = Date.now()
            this.stopTimePoints += this.stopAfter - this.stopBefore
          }
            this.interval = setInterval(() => {
            this.currentPoint = Date.now()
            this.resultTime = Math.floor((this.currentPoint - (this.startPoint + this.stopTimePoints)) / 1000) 
          }, 1000)
        } else {
          clearInterval(this.interval)
          this.stopBefore = Date.now()
        }
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