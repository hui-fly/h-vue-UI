<template>
  <div :class="marqueeCon" class="marquee-con" ref="marqueeConDom"> 
      <div :class="{'marquee-top':marquee_top}" class="marquee" ref="marqueeDom">
          <p class="marquee-item" v-for="(item,index) in marqueeList" :key="index">
              {{item}}
          </p>
      </div>
  </div>
</template>

<style lang="less"> 
    @import './index.less';
    
</style>

<script>
export default {
  name: 'h-marquee',
  data() {
    return{
      marquee_top:false,
    }
  }, 
  components: {},
  props:{
    marqueeCon:{
        type:String,
        default:'marquee-con1'
    },
    marqueeList:{
      type:Array,
      default:[1,2,3,4,5,6]
    },
    time:{
        type:Number,
        default:0.5,
    }
  },
  methods: {
    runMarquee() {
      if(this.marqueeCon==='marquee-con2') {
          this.marqueeList.push(this.marqueeList[0])
          return;
      }
      this.marquee_top=true;
      let marqueeDom = this.$refs.marqueeDom;
      setInterval(()=>{
        this.marquee_top=true;
        marqueeDom.style.marginTop=-this.conHeight+'px'
        marqueeDom.style.transition=this.time+'s';
        setTimeout(()=>{
          marqueeDom.style.marginTop=0;
          marqueeDom.style.transition='';
          this.marqueeList.push(this.marqueeList[0])
          this.marqueeList.shift();
          this.marquee_top = false;
        },this.time*1000)
      },this.time*1000+1000)
    },
    init() {
        let marqueeConDom = this.$refs.marqueeConDom;
        let marqueeDom = this.$refs.marqueeDom;
        let len = this.marqueeList.length-1;
        this.conHeight=marqueeConDom.offsetHeight  //获取计算后的高度
        marqueeConDom.style.lineHeight = this.conHeight+'px'
        marqueeDom.style.height = this.conHeight*len+'px'  //这个是异步的
        if(this.marqueeCon==='marquee-con2'){
            marqueeDom.style.animationDuration=this.time+'s'
        }
    }
  },
  mounted() {
    this.runMarquee();
    this.init()
  }
}
</script>

