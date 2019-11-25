<template>
	<div class="detail-wrap">
		<!-- 左边部分 -->
		<div class="detail-left">
			<img :src="imgSrc">
			<ul>
				<router-link v-for="product in products" tag="li" :to="{path:product.path}" active-class="active">
					{{product.label}}
				</router-link>
				
			</ul>
		</div>
		<!-- 右边部分 -->
		<div class="detail-right">
			<keep-alive>
				<router-view></router-view>
			</keep-alive>
		</div>
	</div>
</template>
<script>
export default{
	data(){
		return {
			products:[
				{
					label:'数据统计',
					path:'count',
					active:false
				},
				{
					label:'数据预测',
					path:'forecast',
					active:false
				},
				{
					label:'流量分析',
					path:'analysis',
					active:false
				},
				{
					label:'广告发布',
					path:'publish',
					active:false
				}
			],
			imgMap:{
				'/detail/count':require('../assets/images/1.png'),
				'/detail/forecast':require('../assets/images/2.png'),
				'/detail/analysis':require('../assets/images/3.png'),
				'/detail/publish':require('../assets/images/4.png')

			}
		}
	},
	computed:{
		imgSrc(){
			return this.imgMap[this.$route.path];
		}
	}
}
</script>
<style>
.detail-wrap{
	margin-top:15px;
	overflow: hidden;

}
.detail-left{
	width:200px;
	float:left;
	margin-right:20px;
	background: #fff;
}
.detail-right{
	width:980px;
	float:left;
}
.detail-left img{
	margin:20px 50px;
}
.detail-left ul{
	padding-bottom:20px;
}
.detail-left ul li{
	height:40px;
	line-height: 40px;
	padding-left:20px;
}
.detail-left ul li:hover,
.detail-left ul li.active{
	background: #4fc08d;
	color:#fff;
}
/*右边样式*/
.sales-board-intro{
	background:#fff;
}
.sales-board-intro h3,
.sales-board-desc h3{
	height:60px;
	line-height: 60px;
	font-size: 22px;
	font-weight: bold;
	padding-left:20px;
}
.sales-board-intro p{
	background:#baf7bc;
	padding:20px;
	line-height: 20px;
}
.sales-board-form{
	background:#fff;
	padding-left:20px;
	padding-top:10px;
}
.sales-board-form .form-line{
	padding:10px 0;
	margin-bottom:10px;
}
.form-line-left{
	display: inline-block;
	width:100px;
}
.form-line-right{
	display: inline-block;
	margin-left:10px;
}

.sales-board-desc{
	background:#fff;
	padding-bottom:20px;
}
.sales-board-desc p{
	padding:20px;
	line-height: 20px;
}
.sales-board-table{
	margin-left:20px;
}
.sales-board-table td{
	padding:20px 25px;
	border:1px solid #e3e3e3;
}
.sales-board-desc h4{
	font-weight: bold;
	font-size: 18px;
	padding-left:20px;
}
.sales-board-desc ul{
	padding:20px;
}
.sales-board-desc ul li{
	line-height: 20px;
}
</style>