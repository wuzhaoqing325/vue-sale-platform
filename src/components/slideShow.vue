<template>
	<div class="slide-show" @mouseover="clearInv" @mouseout="setInv">
		<div class="slide-show-img">
			<transition name="slide-trans">
				<img v-if="isShow" :src="slides[nowIndex].src">
			</transition>
			<transition name="slide-trans-old">
				<img v-if="!isShow" :src="slides[nowIndex].src">
			</transition>
		</div>
		<h2 class="slide-show-title">{{slides[nowIndex].title}}</h2>
		<div class="slide-show-pages">
			<ul>
				<span @click="goto(prevIndex)">&lt;</span>
				<li v-for="(slide,index) in slides" :class="{on: index===nowIndex}" @click="goto(index)">{{index+1 }}</li>
				<span @click="goto(nextIndex)">&gt;</span>
			</ul>
		</div>
	</div>
</template>
<script>
export default{
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
		return {
			nowIndex:0,
			isShow:false,
			timer:null		
		}
	},
	computed:{
		prevIndex(){
			if(this.nowIndex === 0){
				return this.slides.length - 1;
			}
			else{
				return this.nowIndex - 1;
			}
		},
		nextIndex(){
			if(this.nowIndex === this.slides.length - 1){
				return 0;
			}else{
				return this.nowIndex + 1;
			}
		}
	},
	methods:{
		goto(index){
			this.isShow = false;
			setTimeout(() => {
				this.isShow = true;
				this.nowIndex = index;
			},10)
		},
		setInv(){
			this.timer=setInterval(() => {
				this.goto(this.nextIndex);

			},this.inv)
		},
		clearInv(){
			clearInterval(this.timer);
		}
	},
	mounted(){
		this.setInv();
	}
}
</script>
<style>
.slide-trans-enter{
	transform: translateX(900px);
}
.slide-trans-enter-active{
	transition:all .5s;
}
.slide-trans-old-leave-active{
	transition:all .5s;
	transform: translateX(-900px);
}
.slide-show{
	width:900px;
	height:500px;
	overflow: hidden;
	position: relative;
}

.slide-show-img img{
	
	position: absolute;
	top:0;
}
.slide-show-title{
	position: absolute;
	bottom:0;
	width:100%;
	height:40px;
	line-height: 40px;
	opacity: .5;
	color:#fff;
	background: #000;
	padding-left:15px;
}
.slide-show-pages{
	position: absolute;
	bottom:13px;
	right:10px;
	color:#fff;
}
.slide-show-pages li{
	display: inline-block;
	padding:0 15px;
}
.slide-show-pages li.on{
	text-decoration: underline;
}
.slide-show-pages li,
.slide-show-pages span{
	cursor: pointer;
}
</style>