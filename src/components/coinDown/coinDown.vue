<template>
    <div class="">
       <div id="redzone">
       </div>
    </div>
</template>
<style>
    .redBox {
        position: absolute;
        z-index: 50;
        animation: redImg 2s infinite linear;
        -webkit-animation: redImg 2s infinite linear;
        -moz-animation: redImg 2s infinite linear;
        -ms-animation: redImg 2s infinite linear;
        -o-animation: redImg 2s infinite linear;
    }

    .redBox {
        position: fixed;
    }
    .redBox .redBoxImg{
        display: block;
        width: 2rem;
        height: 2.6rem;
    }
    @keyframes redImg {
        0% {
            top:0;
        }
        100% {
            top: 100%;
        }
    }
</style>
<script>
export default {
    name:'hongbao',
    data () {
        return {
          timeOut:'',
          interval:''
        }
    },
    props:{
        redBoxImgSrc:{
            type:String,
            default:require('./images/packet.png')
        },
        timeSpace:{  
            type:Number,
            default:200,
        },
        aniTime:{
            type:Number,
            default:2000,
        },
        dropTime:{
            type:Number,
            default:2000,
        }
    },
    methods:{
        addBao(left, src) {
            let div = document.createElement("div");
            let img = document.createElement("img");
            div.appendChild(img);
            img.className = "redBoxImg";
            img.src = src;
            div.style.left = left + "px";
            div.className = "redBox";
            div.style.animationDuration=this.dropTime+'s',
            document.getElementById("redzone").appendChild(div);
            this.timeOut = setTimeout(()=>{
                document.getElementById("redzone").removeChild(div);
            }, this.dropTime*1000);
        },
    },
    mounted(){
        clearInterval(this.interval)
        this.interval=setInterval(()=>{
            let left = Math.random() * document.body.scrollWidth;;
            let height = Math.random() * document.body.scrollHeight;
            let src = this.redBoxImgSrc; 
            this.addBao(left, src);
        }, this.timeSpace*1000);
        setTimeout(()=>{
            clearInterval(this.interval)
            this.interval=null;
        },this.aniTime*1000)
    }
}
</script>