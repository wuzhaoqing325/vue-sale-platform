<template>
	<div class="sales-board">
		<!-- 上面的介绍部分 -->
		<div class="sales-board-intro">
			<h3>广告发布</h3>
			<p>广告活动按照广告计划执行，到完成广告创作并形成广告作品之后，经过广告主的最后审核同意，即可送到预定的媒介发布刊播。这项工作一般由媒介部门的有关专业人员负责，他们的任务就是专门负责与有关媒介单位接洽，安排有关广告的发播事宜，并对发播质量实施监督。</p>
		</div>
		<!-- 列表部分 -->
		<div class="sales-board-form">
			<!-- 购买数量 -->
			<div class="form-line">
				<div class="form-line-left">
					购买数量：
				</div>
				<div class="form-line-right">
					<counter :max="maxNum" :min="minNum"></counter>
				</div>
			</div>
			<!-- 行业 -->
			<div class="form-line">
				<div class="form-line-left">
					行业：
				</div>
				<div class="form-line-right">
					<selection :selections="jobs"></selection>
				</div>
			</div>
			<!-- 产品版本 -->
			<div class="form-line">
				<div class="form-line-left">
					产品版本：
				</div>
				<div class="form-line-right">
					<multiply-chooser :selections="versionList"></multiply-chooser>
				</div>
			</div>

			<!-- 有效时间 -->
			<div class="form-line">
				<div class="form-line-left">
					有效时间：
				</div>
				<div class="form-line-right">
					一年
				</div>
			</div>
			<!-- 总价 -->
			<div class="form-line">
				<div class="form-line-left">
					总价：
				</div>
				<div class="form-line-right">
					600元
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
			<p>广告活动按照广告计划执行，到完成广告创作并形成广告作品之后，经过广告主的最后审核同意，即可送到预定的媒介发布刊播。这项工作一般由媒介部门的有关专业人员负责，他们的任务就是专门负责与有关媒介单位接洽，安排有关广告的发播事宜，并对发播质量实施监督。</p>
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
import Selection from '../../components/base/selection'
import Counter from '../../components/base/counter'
import MultiplyChooser from '../../components/base/multiplyChooser'
export default{
	components:{
		Selection,
		Counter,
		MultiplyChooser
	},
	data(){
		return{
			maxNum:5,
			minNum:1,
			jobs:[
				{
					label:'出版业',
					value:0
				},
				{
					label:'媒体',
					value:1
				},
				{
					label:'金融',
					value:2
				},
				{
					label:'互联网',
					value:3
				},
				{
					label:'游戏',
					value:4
				}
			],
			versionList:[
				{
					label:'初级版',
					value:0
				},
				{
					label:'中级版',
					value:1
				},
				{
					label:'高级版',
					value:2
				},
				{
					label:'专家版',
					value:3
				}
			]
			}
		}
	}
</script>