<template>
	<div class="counter-component">
		<div class="minus" @click="decrese"> - </div>
		<input type="text" v-model="number">
		<div class="add" @click="increse"> + </div>
	</div>
</template>
<script>
export default{
	props:{
		max:{
			type:Number,
			default:5
		},
		min:{
			type:Number,
			default:1
		}
	},
	data(){
		return {
			number:this.min
		}
	},
	watch:{
		number(){
			this.$emit('on-change',this.number);
		}
	},
	methods:{
		decrese(){
			if(this.number <= this.min){
				return 
			}
				this.number --;
		},
		increse(){
			if(this.number >= this.max){
				return 
			}
				this.number ++;
		}
	}
}
</script>
<style>

.counter-component input{
	border:none;
	width:26px;
	height:26px;
	padding:0;
	line-height: 26px;
	text-align: center;
	outline: none;
	float:left;
	border-top:1px solid #e3e3e3;
	border-bottom:1px solid #e3e3e3;
}
.minus,.add{
	width:26px;
	height:26px;
	display: inline-block;	
	float:left;
	border: 1px solid #e3e3e3;
	line-height: 26px;
	text-align: center;
	cursor:pointer;
}	
</style>