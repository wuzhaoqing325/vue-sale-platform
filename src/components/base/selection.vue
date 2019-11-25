<template>
	<div class="selection-component">
		<div class="selection-show" @click="toggleDrop">
			<span>{{selections[nowIndex].label}}</span>
			<div class="drop"></div>
		</div>
		<div>
			<ul class="selection-list" v-if="isDrop">
				<li v-for="(item,index) in selections" @click="changeSelection(index)">
					{{item.label}}
				</li>
			</ul>
		</div>
	</div>
</template>
<script>
export default{
	props:{
		selections:{
			type:Array,
			default:[]
		}

	},
	data(){
		return {
			nowIndex:0,
			isDrop:false
		}
	},
	methods:{
		toggleDrop(){
			this.isDrop = !this.isDrop;
		},
		changeSelection(index){
			this.nowIndex = index;
			this.isDrop = false;
			this.$emit('on-change',this.selections[index]);
		}
	}
}
</script>
<style>
.selection-component{
	position: relative;
	display: inline-block;
}
.selection-show{
	height:25px;
	line-height: 25px;
	border:1px solid #e3e3e3;
	padding:0 20px 0 10px;
	border-radius: 3px;
	cursor: pointer;
	position: relative;
	background: #fff;
}
.selection-show .drop{
	display: inline-block;
	width:0;
	height: 0;
	border-left:4px solid transparent;
	border-right:4px solid transparent;
	border-top:5px solid #e3e3e3 ;
	margin-top:-1px;
	margin-left:6px;
	margin-right: -14px;
	vertical-align: middle;
}
.selection-list{
	width:100%;
	border-bottom:1px solid #e3e3e3;
	position: absolute;
	top:25px;
	left:0;
	z-index: 5px;
	background: #fff;
}
.selection-list li{
	height:25px;
	line-height: 25px;
	padding-left:10px;
	border-right:1px solid #e3e3e3;
	border-left:1px solid #e3e3e3;
	cursor: pointer;
}
.selection-list li:hover{
	background: #e3e3e3;
}
</style>