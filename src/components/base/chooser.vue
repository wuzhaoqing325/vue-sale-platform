<template>
	<div class="chooser-component">
		<ul>
			<li v-for="(item,index) in selections" :class="{'active': index === nowIndex}" @click="changeSelection(index)">
				{{item.label}}
			</li>
		</ul>
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
			nowIndex:0
		}
	},
	methods:{
		changeSelection(index){
			this.nowIndex = index;
			this.$emit('on-change',this.selections[index]);
		}
	}
}
</script>
<style>
.chooser-component li{
	display: inline-block;
	border:1px solid #e3e3e3;
	padding:6px 9px;
	border-radius: 3px;
	margin-right:10px;
	cursor:pointer;
}
.chooser-component li.active{
	background:  #4fc08d;
}
</style>