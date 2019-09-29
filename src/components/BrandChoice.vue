<template>
  <div class="choice" @click="clickHandler">
    <transition name="fade">
      <img v-if="incorrect" :src="require('@/assets/cross.png')" class="incorrect">
    </transition>
    <img :src="image" :alt="brand">
  </div>
</template>

<script>
export default {
  name: 'BrandChoice',
  props: ['brand', 'image', 'incorrectChoices'],
  data() {
    return { clicked: false }
  },
  computed: {
    incorrect: function() {
      return this.incorrectChoices.some(choice => choice === this.brand)
    }
  },
  methods: {
    clickHandler() {
      this.clicked = true;
      this.$emit('brand-clicked', this.brand)
    }
  }
}
</script>

<style>
.choice{
  position: relative;
}
.choice:first-child{
  order: 5;
}
.choice:last-child{
  order: 2;
}
.choice img{
  width: 70px;
  cursor: pointer;
}
.choice img.incorrect{
  position: absolute;
  width: 20px;
  top: 40%;
  left: -10px;
}

</style>
