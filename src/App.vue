<template>
  <div id="app">

    <header>
      <div class="hero hero-sm">
        <h1>Take our brands quiz</h1>
        <h4>Can you guess who made the products below?</h4>
      </div>
      <ul class="tab">
        <li class="tab-item active"><a href="#">Trainers</a></li>
        <li class="tab-item"><a href="#">Suits</a></li>
        <li class="tab-item"><a href="#">Workwear</a></li>
        <li class="tab-item"><a href="#">Jeans</a></li>
      </ul>
    </header>

    <div class="game">

      <div class="feedback">
        <button v-if="!isActive && !hasWon" @click="start">{{this.message}}</button>
        <samp v-if="isActive">00:{{ this.paddedSeconds() }}s</samp>
        <strong v-if="!isActive && hasWon">{{this.message}}</strong>
      </div>
      
      <div class="tiles" :class="{ playing: isActive }">
        <Tile 
          v-for="item in this.data" 
          :key="item.brand"
          :brand="item.brand" 
          :image="item.image"
          :pairs="pairs" 
          :selected="tileSelected" 
          @tile-clicked="handleTileClick">
        </Tile>
      </div>
      <transition name="slide-fade">
        <div class="choices" v-if="tileSelected">
          <BrandChoice 
            v-for="item in this.data" 
            :key="item.brand"
            :brand="item.brand"
            :incorrectChoices="incorrectChoices" 
            :image="item.logo"
            @brand-clicked="handleBrandClick">
          </BrandChoice>
        </div>
      </transition>

    </div>

  </div>
</template>

<script>
import Tile from './components/Tile.vue'
import BrandChoice from './components/BrandChoice.vue'
import data from './data/example_data'

export default {
  name: 'app',
  components: {
    Tile,
    BrandChoice
  },
  data() {
    return {
      isActive: false,
      timer: null,
      hasWon: false,
      seconds: 30,
      tileSelected: null,
      message: 'Start',
      pairs: [],
      incorrectChoices: [],
      data
    }
  },

  methods: {
    start() {
      this.isActive = true
      this.timer = setInterval(this.timerLogic, 1000)
    },
    timerLogic() {
      this.seconds -= 1;
      if (this.haswon) this.triggerWin()
      if (this.seconds === 0) this.triggerLoss()
    },
    stop() {
      this.isActive = false
      this.seconds = 30
      clearInterval(this.timer)
      this.pairs = []
      this.tileSelected = null
    },
    triggerWin(){
      this.stop()
      this.hasWon = true
      this.message = 'Great work!!'
    },
    triggerLoss(){
      this.stop()
      this.message = 'Try again'
    },
    handleTileClick(tile) {
      if(!this.isActive) return
      //toggle the tile choice
      this.tileSelected = this.tileSelected === tile ? null : tile
      //wipe any incorrect choices
      this.incorrectChoices = []
    },
    paddedSeconds(){
      return this.seconds < 10 ? `0${this.seconds}` : this.seconds
    },
    handleBrandClick(brand) {
      if(!this.isActive) return
 
      //detect a succesful pairing
      if(this.tileSelected === brand) {
        this.pairs.push(brand)
        this.tileSelected = null
      }
      //detect an unsuccesful pairing
      if(this.tileSelected !== brand) this.incorrectChoices.push(brand)

      //detect win conditions
      if (this.pairs.length === data.length) this.triggerWin()
    }
  }
}
</script>
// background-color: #FFFFFF;
// background-image: linear-gradient(165deg, #FFFFFF 0%, #6284FF 50%, #FF0000 100%);

<style>
header{
  background: linear-gradient(170deg, #df8e16 0%, #e64b33 45%, #e64b33 55%,  #df8e16 100%);
  color: white !important;
  padding-top: 2em;
}
header .tab .tab-item.active a,
header .tab .tab-item a,
header .tab .tab-item a:active,
header .tab .tab-item a:focus,
header .tab .tab-item a:hover{
  color: white;
  box-shadow: none;
  margin-right: 20px;
}
header .tab .tab-item.active a{
  color: #3d3d3d;
  font-weight: 700;
  border-bottom-color: #3d3d3d;
  border-bottom-width: 3px;
}
.tab{
  justify-content: center;
  margin: 0 !important;
}
h1{
  text-transform: uppercase;
  letter-spacing: 6px;
}
h4{
  font-weight: 300 !important; 
  letter-spacing: -1px;
}
.game{
  margin-bottom: 30px;
}
button{
  background: #e64b33;
  color: white;
  padding: 5px 15px;
  border-radius: 20px;
}
.feedback{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  background-color: #ddd;
}
.tiles {
  min-width: 100%;
  height: 240px;
  background: linear-gradient(#ddd 0%, #df8e16 45%, #e64b33 78%, #3d3d3d 78%, #fff 90%);
  /* background: linear-gradient(170deg, #000 0%, #e64b33 45%, #e64b33 55%,  #000 100%); */
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  overflow-x: scroll; 
  overflow-y: hidden; 
}
.tiles::-webkit-scrollbar { 
  display: none; 
} 
.choices{
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  height: 100px;
  width: 100%;
  background-color: #ddd;
  margin: 0 auto;
}

</style>
