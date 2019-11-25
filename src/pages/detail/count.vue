<template>
	<div class="sales-board">
		<!-- 上面的介绍部分 -->
		<div class="sales-board-intro">
			<h3>数据统计</h3>
			<p>历史资料、科学实验、检验、统计等所获得的和用于科学研究、技术设计、查证、决策等的数值加以统计为解决方案做前期准备。</p>
		</div>
		<!-- 列表部分 -->
		<div class="sales-board-form">
			<!-- 产品类型 -->
			<div class="form-line">
				<div class="form-line-left">
					产品类型：
				</div>
				<div class="form-line-right">
					<chooser :selections="versions"></chooser>
				</div>
			</div>
			<!-- 适用地区 -->
			<div class="form-line">
				<div class="form-line-left">
					适用地区：
				</div>
				<div class="form-line-right">
					<selection :selections="citys"></selection>
				</div>
			</div>
			<!-- 有效时间 -->
			<div class="form-line">
				<div class="form-line-left">
					有效时间：
				</div>
				<div class="form-line-right">
					半年
				</div>
			</div>
			<!-- 总价 -->
			<div class="form-line">
				<div class="form-line-left">
					总价：
				</div>
				<div class="form-line-right">
					500元
				</div>
			</div>
			<!-- 立即购买 -->
			<div class="form-line">
				<div class="form-line-left">
					
				</div>
				<div class="form-line-right">
					<div class="button">立即购买</div>
				</div>
			</div>
		</div>
		<!-- 产品说明部分 -->
		<div class="sales-board-desc">
			<h3>产品说明</h3>
			<p>历史资料、科学实验、检验、统计等所获得的和用于科学研究、技术设计、查证、决策等的数值加以统计为解决方案做前期准备。</p>
			<div class="sales-board-table">
				<table>
					<tr>
						<td>安全安保</td>
						<td>办公文教</td>
						<td>彩票</td>
						<td>车辆</td>
						<td>成人用品</td>
						<td>出版传媒</td>
						<td>电脑硬件</td>
					</tr>
					<tr>
						<td>安全安保</td>
						<td>办公文教</td>
						<td>彩票</td>
						<td>车辆</td>
						<td>成人用品</td>
						<td>出版传媒</td>
						<td>电脑硬件</td>
					</tr>
					<tr>
						<td>安全安保</td>
						<td>办公文教</td>
						<td>彩票</td>
						<td>车辆</td>
						<td>成人用品</td>
						<td>出版传媒</td>
						<td>电脑硬件</td>
					</tr>
					<tr>
						<td>安全安保</td>
						<td>办公文教</td>
						<td>彩票</td>
						<td>车辆</td>
						<td>成人用品</td>
						<td>出版传媒</td>
						<td>电脑硬件</td>
					</tr>
					<tr>
						<td>安全安保</td>
						<td>办公文教</td>
						<td>彩票</td>
						<td>车辆</td>
						<td>成人用品</td>
						<td>出版传媒</td>
						<td>电脑硬件</td>
					</tr>
				</table>
			</div>
		</div>
	</div>
</template>
<script>
import Chooser from '../../components/base/chooser'
import Selection from '../../components/base/selection'
export default{
	components:{
		Chooser,
		Selection
	},
	data(){
		return {
			versions:[
				{
					label:'红色版',
					value:0
				},
				{
					label:'绿色版',
					value:1
				},
				{
					label:'紫色版',
					value:2
				}

			],
			citys:[
				{
					label:'北京',
					value:0
				},
				{
					label:'上海',
					value:1
				},
				{
					label:'广州',
					value:2
				},
				{
					label:'天津',
					value:3
				},
				{
					label:'武汉',
					value:4
				},
				{
					label:'重庆',
					value:5
				}
			]
		}
	}
}
</script>
<style scoped>
	
</style>