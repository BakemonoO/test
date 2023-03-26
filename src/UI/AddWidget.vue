<template>
  <div class="add-widget"
  @click="$emit('createWidget')"
  >
    <div>
      <div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'add-widget'
  }
</script>

<style lang="scss" scoped>

.add-widget {
  height: 120px;
  width: 255px;
  background: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 50px;
  &:hover {
    div {
      background: #FFFFFF;
    } 
    }
  div {
    background: #9E9E9E;
    height: 3px;
    width: 20px;
    div {
    background: #9E9E9E;
    transform: rotate(90deg);
    }
  }
  }


</style>