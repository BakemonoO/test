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
  padding-top: 70px;
  min-height: 100vh;
}

</style>
