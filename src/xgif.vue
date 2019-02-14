<style lang="scss">
@import "./xgif.scss";
</style>
<template>
<div class="x-gif">
    <img id="" :data-animated-src="src" data-autoplay="0" ref="gif"/>
    <div class="button-group">
        <button class="button1"> 播放 </button>
        <button class="button1" @click="reset">重置</span> </button>
        <button class="button1" @click="nextStep"> 下一帧</span> </button>
        <button class="button1" @click="preStep">上一帧</span> </button>
        <button class="button1" @click="">跳转</button>
        <div class="inputClass">
            <input v-model="frame" type="number"></input><span>/</span><span>{{frameLength}}帧</span>
        </div>
    </div>
</div>
</template>
<script>
//import supergif from './sibgif/sibgif.js'
var SuperGif  = require('./sibgif/sibgif.js')
export default {
    data() {
        return {
            sup:null,
            frame:0,
        }
    },
    props:{
        autoload:{   // 自动加载
            type:Boolean,
            default:false
        },
        src:{
            type:String,
            default:""
        }
    },
    computed:{
        frameLength(){
            if( this.sup){
                return this.sup.get_length()
            }
            return 0
        },
        gidx(){
            if( this.sup){
                 return this.sup.get_current_frame()
            }
            return 0
        },
    },
    methods:{
        idx(){
            if( this.sup){
                
                let i = this.sup.get_current_frame();
                console.log(i)
                this.frame = parseInt(i)
            }
            else
                this.frame = 3
        },
        play(){
            if( this.sup !== null){
                this.sup.play()
            }
        },
        nextStep(){
            if( this.sup !== null){
                this.sup.move_relative(1)
                this.idx()
            }
        },
        preStep(){
            if( this.sup !== null){
                this.sup.move_relative(-1)
                this.idx()
            }
        },
        reset(){
            if( this.sup !== null){
                this.sup.move_to(0)
                this.idx()
            }
        }

    },
    mounted(){
        let gifDom = this.$refs.gif
        var sup2 = new SuperGif({ gif:gifDom , includeDataURL: true } );
		sup2.load((err, gif)=>{
			if (err) {console.log(err);}
			this.sup = sup2
			console.log(sup2.get_frames().length);
		});
    }

}
</script>
