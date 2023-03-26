<template>
  <div class="widget-list">
    <transition-group name="widget-list">
    <time-widget
    v-for="widget in widgetArray"
    :key="widget.id"
    :timeSet="widget.timeSet"
    />
    <add-widget
    @create-widget="createWidget"
    :key="'addWidget'"
    />
    </transition-group>
  </div>
</template>

<script>
import AddWidget from './UI/AddWidget.vue'
import TimeWidget from './UI/TimeWidget.vue'
  export default {
  components: { TimeWidget, AddWidget },
    name: 'widget-list',

    data() {
      return {
        widgetArray: [{id:1, timeSet: [1,32,1]}, {id:2, timeSet: [0,4,32]}, {id:3}]
      }
    },

    methods: {
      createWidget() {
        const widgetId = this.widgetArray[this.widgetArray.length - 1].id + 1
        this.widgetArray.push({id: widgetId})

      }
    }
  }
</script>

<style lang="scss" scoped>

.widget-list {
  display: grid;
  width: 85%;
  min-height: 250px;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  grid-row-gap: 45px;
  justify-items: center;
}

.widget-list-item {
  display: inline-block;
  margin-right: 10px;
}
.widget-list-enter-active,
.widget-list-leave-active {
  transition: all 1s ease;
}
.widget-list-enter-from,
.widget-list-leave-to {
  opacity: 0;
}

.widget-list-move {
  transition: transform 0.5s ease;
}

</style>