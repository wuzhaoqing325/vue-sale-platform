<template>
	<div class="sales-board">
		<!-- 上面的介绍部分 -->
		<div class="sales-board-intro">
			<h3>流量分析</h3>
			<p>是指在获得网站访问量基本数据的情况下对有关数据进行统计、分析，从中发现用户访问网站的规律，并将这些规律与网络营销策略等相结合，从而发现目前网络营销活动中可能存在的问题，并为进一步修正或重新制定网络营销策略提供依据。当然这样的定义是站在网络营销管理的角度来考虑的</p>
		</div>
		<!-- 列表部分 -->
		<div class="sales-board-form">
			<!-- 购买数量 -->
			<div class="form-line">
				<div class="form-line-left">
					购买数量：
				</div>
				<div class="form-line-right">
					<counter :max="maxNum" :min="minNum" @on-change="onParamChange('buyNum',$event)"></counter>
				</div>
			</div>
			<!-- 产品类型 -->
			<div class="form-line">
				<div class="form-line-left">
					产品类型：
				</div>
				<div class="form-line-right">
					<selection :selections="productTypes" @on-change="onParamChange('productType',$event)"></selection>
				</div>
			</div>
			<!-- 有效时间 -->
			<div class="form-line">
				<div class="form-line-left">
					有效时间：
				</div>
				<div class="form-line-right">
					<chooser :selections="periodList" @on-change="onParamChange('period',$event)"></chooser>
				</div>
			</div>
			<!-- 产品版本 -->
			<div class="form-line">
				<div class="form-line-left">
					产品版本：
				</div>
				<div class="form-line-right">
					<multiply-chooser :selections="versionsList" @on-change="onParamChange('versions',$event)"></multiply-chooser>
				</div>
			</div>
			
			<!-- 总价 -->
			<div class="form-line">
				<div class="form-line-left">
					总价：
				</div>
				<div class="form-line-right">
					{{ price }}元
				</div>
			</div>
			<!-- 立即购买 -->
			<div class="form-line">
				<div class="form-line-left">
					
				</div>
				<div class="form-line-right">
					<div class="button" @click="showPayDialog">立即购买</div>
				</div>
			</div>
		</div>

		<!-- 产品说明部分 -->
		<div class="sales-board-desc">
			<h3>产品说明</h3>
			<p>网站访问统计分析报告的基础数据源于网站流量统计信息，但其价值远高于原始数据资料。专业的网站访问统计分析报告对网络营销的价值，正如专业的财务分析报告对企业经营策略的价值。</p>
			<h4>用户行为指示</h4>
			<ul>
				<li>用户行为指标主要反映用户是如何来到网站的、在网站上停留了多长时间、访问了哪些页面等，主要的统计指标包括：</li>
				<li>用户在网站的停留时间；</li>
				<li>用户来源网站（也叫“引导网站”）；</li>
				<li>用户所使用的搜索引擎及其关键词；</li>
				<li>在不同时段的用户访问量情况等。</li>
			</ul>

			<h4>浏览网站方式</h4>
			<ul>
				<li>用户上网设备类型</li>
				<li>用户浏览器的名称和版本</li>
				<li>访问者电脑分辨率显示模式</li>
				<li>用户所使用的操作系统名称和版本</li>
				<li>用户所在地理区域分布状况等</li>
			</ul>
		</div>
		<!-- 选择银行的对话框 -->
		<my-dialog :is-show="isShowPayDialog" @on-close="hidePayDialog" class="pay-dialog">
			
			<table class="payTable">
				<thead>
					<tr>
						<th>购买数量</th>
						<th>产品类型</th>
						<th>有效时间</th>
						<th>产品版本</th>
						<th>总价</th>
					</tr>
				</thead>
				<tbody>
					<tr>
					<td>{{ buyNum }}</td>
					<td>{{ productType.label }}</td>
					<td>{{ period.label }}</td>
					<td>
						<span v-for="version in versions">{{ version.label }}</span>
					</td>
					<td>{{ price }}</td>
				</tr>
				</tbody>
			</table>
			<h3>请选择银行</h3>
			
			<bank-chooser @on-change="onChangeBank"></bank-chooser>
			<div class="button pay-dialog-btn" @click="confirmBuy">确认购买</div>
		</my-dialog>

		<!-- 检查支付状态的对话框 -->
		<check-order :is-show-check-dialog="isShowCheckOrder" :order-id="orderId" @on-close-check-dialog="hideCheckOrder"></check-order>


	</div>
</template>
<script>

import Counter from '../../components/base/counter'
import Selection from '../../components/base/selection'
import Chooser from '../../components/base/chooser'
import MultiplyChooser from '../../components/base/multiplyChooser'
import MyDialog from '../../components/base/dialog'
import BankChooser from '../../components/bankChooser'
import CheckOrder from '../../components/checkOrder'
import _ from 'lodash'
export default{
	components:{
		Counter,
		Selection,
		MultiplyChooser,
		Chooser,
		MyDialog,
		BankChooser,
		CheckOrder

	},
	data(){
		return{
			maxNum:5,
			minNum:1,
			productTypes:[
				{
					label:'入门级',
					value:0
				},
				{
					label:'中级级',
					value:1
				},
				{
					label:'高级级',
					value:2
				}
			],
			periodList:[
				{
					label:'半年',
					value:0
				},
				{
					label:'一年',
					value:1
				},
				{
					label:'三年',
					value:2
				}

			],
			versionsList:[
				{
					label:'客户版',
					value:0
				},
				{
					label:'代理商版',
					value:1
				},
				{
					label:'专家版',
					value:2
				}

			],
			isShowPayDialog:false,
			buyNum:0,
			productType:{},
			period:{},
			versions:[],
			price:100,
			isShowCheckOrder:false,
			bankId:null,
			orderId:null
			
			
			}
		},
		methods:{
			showPayDialog(){
				this.isShowPayDialog = true;
			},
			hidePayDialog(){
				this.isShowPayDialog = false;
			},
			onParamChange(attr,val){
				this[attr] = val;
				this.getPrice();
			},
			getPrice(){
				this.$http.get('../../static/db.json').then((res) => {
					this.price = res.data.getPrice.amount;
				},(error) => {
					console.log(error);
				})
				
			},
			confirmBuy(){
				let buyVersionArray = _.map(this.version,(item) => {
					return item.value;
				}) 
				let reqParams = {
					buyNum:this.buyNum,
					productType:this.productType,
					period:this.period,
					version:buyVersionArray.join(','),
					bankId:this.bankId
				}
				this.$http.get('../static/db.json').then((res) => {
					this.orderId = res.data.createOrder.orderId;
				},(error) => {
					console.log(error);
				})

				this.isShowCheckOrder = true;
				this.hidePayDialog();
			},
			hideCheckOrder(){
				this.isShowCheckOrder = false;
			},
			onChangeBank(bankObj){
				this.bankId = bankObj.id;
			}
			
		},
		mounted(){
			this.buyNum = 1;
			this.productType = this.productTypes[0];
			this.period = this.periodList[0];
			this.versions = [this.versionsList[0]];		
		}

	}
</script>
<style>
.payTable{
	width:100%;
}
.payTable tr{
	height:30px;
	line-height: 30px;
}
.payTable thead{
	background: #4fc08d;
}
.payTable td,
.payTable th{
	text-align: center;
}
.payTable td{
	border:1px solid #e3e3e3;
}
.payTable thead{
	border:1px solid #4fc08d;
}
.pay-dialog h3{
	font-size: 16px;
	font-weight: bold;
	margin:20px 0 10px 0;
}
.pay-dialog-btn{
	margin-top:10px;
	padding:12px 17px;
}

</style>