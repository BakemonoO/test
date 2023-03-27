<template>
<div class="widget-app">
  <widget-list/>
</div>
</template>

<script>
import WidgetList from './WidgetList.vue'

export default {
  components: { WidgetList },
  name: 'App',

  data() {
    return {
      startPoint: null,
      newDate: null,
      resultTime: null,
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

    getResult() {
      if (this.startPoint !== null && this.newDate !== null && this.resultTime !== null) {
          const currentSecconds = this.resultTime - (this.getHours * 3600) - (this.getMinutes * 60)
          return `прошло ${this.getHours} часов, ${this.getMinutes} минут, ${currentSecconds} секунд`
      }
    }
  },

  mounted() {
    // this.startPoint = Math.floor(Date.now() / 1000)
    // setInterval(() => {
    //   this.newDate = Math.floor(Date.now() / 1000)
    //   this.resultTime = this.newDate - this.startPoint
    //   console.log(this.getResult)
    // }, 1000);
   
  }
}
</script>

<style lang="scss">

@font-face {
  font-family: 'GothamPro';
  src: url(fonts/gothampro.ttf);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'GothamPro';
  font-weight: 400;
  line-height: 21px;
  font-size: 21px;
}

.widget-app {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  background: #353638;
  padding: 70px 0;
  min-height: 100vh;
}

</style>
