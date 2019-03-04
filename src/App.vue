<template>
  <div class="app">
    <div class="con">
      <h-marquee :marqueeList='list'
          :marqueeCon='marqueeDom'
          :time='time'
          >
      </h-marquee>
    </div>
    <h-coinDown 
        :dropTime=2
        :aniTime=3
        :timeSpace=0.1
        >
    </h-coinDown>
  </div>
</template>

<style>
  .con{
    position: relative;
    height: 70px;
    background: #ff8;
    top:100px;
  }
</style>

<script>
import HMarquee from './components/marquee/marquee.vue'
import HcoinDown from './components/coinDown/coinDown.vue'
export default {
  name: 'app',
  components:{
    'h-marquee':HMarquee,
    'h-coinDown':HcoinDown,
  },
  data() {
    return{
      list:[1,2,3,4,5],
      marqueeDom:'marquee-con2',
      time:5
    }
  },
}
</script>

