<template>
	<div class="bankChooser-component">
		<ul>
			<li v-for="(bank,index) in banks" 
			:class="[bank.name,{active: index===nowIndex }]"
			@click="changeBank(index)"
			:title="bank.label"
			></li>
		</ul>
	</div>
</template>
<script>
export default{
	data(){
		return{
			nowIndex:0,
			banks:[
				{	
					id:0,
					label:'兴业银行',
					name:'xinye'
				},
				{
					id:1,
					label:'中信银行',
					name:'zhongxin'
				},
				{
					id:2,
					label:'中国建设银行',
					name:'jianshe'
				},
				{
					id:3,
					label:'广发银行',
					name:'guangfa'
				},
				{
					id:4,
					label:'北京银行',
					name:'beijing'
				},
				{
					id:5,
					label:'中国农业银行',
					name:'nongye'
				},
				{
					id:6,
					label:'浦发银行',
					name:'pufa'
				},
				{
					id:7,
					label:'中国银行',
					name:'zhongguo'
				}
			]
		}
	},
	methods:{
		changeBank(index){
			this.nowIndex = index;
			this.$emit('on-change',this.banks[index]);
		}
	}
}
</script>
<style>
.bankChooser-component{
	width:90%;
}
.bankChooser-component li{
	display: inline-block;
	background-image: url('../assets/banks/banks.png');
	background-repeat: no-repeat;
	width:117px;
	height:32px;
	margin:5px;
	cursor: pointer;
	border:1px solid #e3e3e3;
}
.bankChooser-component li.active{
	border:1px solid #4fc08d;
}
.xinye{
	background-position: 0 0;
}
.zhongxin{
	background-position: -480px 0;
}
.jianshe{
	background-position: -720px 0;
}
.guangfa{
	background-position: -840px 0;
}
.beijing{
	background-position: -960px 0;
}
.nongye{
	background-position: -1680px 0;
}
.pufa{
	background-position: -1800px 0;
}
.zhongguo{
	background-position: -2520px 0;
}
</style>
