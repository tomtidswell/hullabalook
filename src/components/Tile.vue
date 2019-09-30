<template>
  <div class="tile" :class="{complete: complete, active: selected === brand}" @click="clickHandler">
    <img v-if="complete" :src="require('@/assets/tick.png')" class="correct">
    <img :src="image" :alt="brand">
    <transition name="slide-fade">
      <div class="arrows" v-if="selected === brand">
        <div class="left"></div>
        <div class="right"></div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'Tile',
  props: ['brand', 'selected', 'pairs', 'image'],
  computed: {
    complete: function() {
      return this.pairs.some(pair => pair === this.brand)
    }
  },
  methods: {
    clickHandler() {
      //only allow the click handler if the tile isnt already matched
      if(!this.complete) this.$emit('tile-clicked', this.brand)
    }
  }
}
</script>

<style scoped>
.tile{
  position: relative;
  display: flex;
  align-items: center;
  background-color: white;
  width: 200px;
  height: 200px;
  margin: 10px;
  box-shadow: 0 0.25rem 1rem rgba(48,55,66,.3);
  transition: all 1s;
}
.tile.active{
  transform: scale(1.1) translateY(-7px);
}

.tiles.playing .tile{
  cursor: pointer;
}

.tile.complete{
  cursor: auto;
  opacity: 0.7;
}

.tile.complete .correct{
  position: absolute;
  width: 50px;
  bottom: 5px;
  left: 5px;
}

.tile img{
  width:100%;
}

.arrows{
  display: flex;
  justify-content: center;
  position: absolute;
  left: calc(50% - 20px);
  bottom: -20px;
}

.arrows .left{
  background: linear-gradient(-45deg, #ddd 0%, #ddd 50%, rgba(255, 255, 255, 0.1) 50%);
  width: 20px;
  height: 20px;
}
.arrows .right{
  background: linear-gradient(45deg, #ddd 0%, #ddd 50%, rgba(255, 255, 255, 0.1) 50%);
  width: 20px;
  height: 20px;
}
</style>

