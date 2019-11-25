<template>
	<div class="mulChooser-component">
		<ul>
			<li v-for="(media,index) in selections" 
			@click="toggleChoose(index)"
			:class="{active:checkActive(index)}"
			>
				{{ media.label }}
			</li>
		</ul>
	</div>
</template>
<script>
import _ from 'lodash'
export default{
	props:{
		selections:{
			type:Array,
			default:[]
		}
	},
	data(){
		return {
			nowIndexs:[0]
		}
	},
	methods:{
		toggleChoose(index){
			// 该下标不在选中的数组中
			if(this.nowIndexs.indexOf(index) === -1){
				this.nowIndexs.push(index);
			}else{
				this.nowIndexs = _.remove(this.nowIndexs,(idx) => {
					return idx !== index;
				})
			}
			let nowObjArray = _.map(this.nowIndexs,(idx) => {
					return this.selections[idx];
			})
			this.$emit('on-change',nowObjArray);

		},
		checkActive(index){
			return this.nowIndexs.indexOf(index) !== -1;
		}

	}
}
</script>
<style>
.mulChooser-component li{
	display: inline-block;
	border:1px solid #e3e3e3;
	padding:6px 9px;
	margin-right:8px;
	border-radius:3px;
	cursor:pointer;
}
.mulChooser-component li.active{
	background: #4fc08d;
}
</style>