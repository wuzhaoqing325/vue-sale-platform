<template>
	<div>
	<div class="dialog-wrap">
		<div class="dialog-cover" @click="closeMyself" v-if="isShow"></div>
		<transition name="drop">
		<div class="dialog-content" v-if="isShow">
			<p class="dialog-close" @click="closeMyself">X</p>
				<slot>empty</slot>
		</div>
		</transition>
	</div>
	</div>
</template>
<script>
export default{
	props:{
		isShow:{
			type:Boolean,
			default:false
		}
	},
	data(){
		return {
			
		}
	},
	methods:{
		closeMyself(){
			this.$emit('on-close');
		}
	}
}
</script>

<style scoped>
.drop-enter-active {
  transition: all .5s ease;
}
.drop-leave-active {
  transition: all .3s ease;
}
.drop-enter {
  transform: translateY(-500px);
}
.drop-leave-active {
  transform: translateY(-500px);
}

.dialog-wrap{
	position: fixed;
	width:100%;
	height:100%;
}
.dialog-cover{
	position: fixed;
	top:0;
	left:0;
	width:100%;
	height:100%;
	background: #000;
	opacity: .3;
	z-index: 5;
}
.dialog-content{
	position: fixed;
	top:20%;
	left:50%;
	margin-left:-25%;
	width:50%;
	max-height: 50%;
	background: #fff;
	border:2px solid #464068;
	overflow: hidden;
	z-index: 10;
	padding:2%;
	line-height: 1.6;
}
.dialog-close{
	position: absolute;
	top:5px;
	right:5px;
	cursor: pointer;
	width:20px;
	height:20px;
	line-height: 20px;
	text-align: center;
}

</style>