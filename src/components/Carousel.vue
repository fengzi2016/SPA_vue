<template>
    <div class="slide-show" @mouseover='clear' @mouseout='run'>
        <div class="slide-img">
            <transition name="slide-trans">
                <a :href='slides[nowIndex].link'>
                    <img v-if="isShow" :src="slides[nowIndex].url">
                </a>
            </transition>
            <transition name="slide-trans-old">
                <a :href='slides[nowIndex].link'>
                    <img v-if="!isShow" :src="slides[nowIndex].url">
                </a>
            </transition>
        </div>
        <ul class="slide-pages">
            <li @click="goto(prevIndex)">
                &lt;
            </li>
            <li v-for="(item,index) in slides" @click="goto(index)" :key="index">
                <a :class="{on: index === nowIndex}">{{index+1}}</a>
            </li>
            <li @click="goto(nextIndex)">&gt;</li>
        </ul>
    </div>
</template>
<<script>
export default {
  props:{
      slides:{
          type:Array,
          default:[]
      },
      inv:{
          type:Number,
          default:1000
      }
  },
  data(){
      return{
          nowIndex:0,
          isShow:true
      }
  },
  computed:{
      prevIndex(){
          if(this.nowIndex===0){
              return this.slides.length-1;
          }
          else{
              return this.nowIndex-1;
          }
      },
      nextIndex(){
          if(this.nowIndex===this.slides.length-1){
            return 0;
          }
          else{
              return this.nowIndex+1;
          }   
      }
  },    
 
  methods: {
    goto (index) {
      this.isShow = false
      setTimeout(() => {
        this.isShow = true
        this.nowIndex = index
      }, 2000)
    },
    run () {
      this.invId = setInterval(() => {
        this.goto(this.nextIndex)
      }, this.inv)
    },
    clear () {
      clearInterval(this.invId)
    }
  },
  mounted () {
    this.run();
  }

}
</script>
<style scoped>
.slide-trans-enter-active {
    transition: all 2s linear ;
}

.slide-trans-enter {
    transform: translateX(1280px);
}

.slide-trans-old-leave-active {
    transition: all  2s linear;
    transform: translateX(-1280px);
}

.slide-show {
    position: relative;
    margin: 15px 15px 15px 0;
    width: 1280px;
    height: 2000px;
    overflow: hidden;
}

.slide-img {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
}

.slide-pages {
    text-align: center;
}

.slide-pages li {
    display: inline;
    padding: 0 10px;
    cursor: pointer;
    color: #fff;
}

.slide-pages li .on {
    text-decoration: underline;
}
</style>


