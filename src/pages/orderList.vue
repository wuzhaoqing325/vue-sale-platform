<template>
	<div class="orderList">
		<h3>您的产品</h3>
		<div class="order-list-choose">
			<!-- 选择产品 -->
			<div class="order-list-option">
				选择产品：
					<selection :selections="products" @on-change="changeProductId"></selection>
			</div>
			<!-- 开始日期 -->
			<div class="order-list-option">
				开始日期：
					<date-picker @on-change="changeStartDate"></date-picker>
			</div>
			<!-- 结束日期 -->
			<div class="order-list-option">
				结束日期：
					<date-picker @on-change="changeEndDate"></date-picker>
			</div>
			<!-- 关键词 -->
			<div class="order-list-option">
				关键词：
					<input type="text" class="query" v-model.lazy="query">
			</div>
		</div>
		<!-- 表格 -->
		<div class="order-list-table">
			<table>
				<thead>
					<th v-for="head in headList" @click="changeOrderType(head)" :class="{active: head.active}">
						{{ head.label }}
					</th>
				</thead>
				<tbody>
					<tr v-for="order in orderList">
						<td v-for="head in headList">{{ order[head.name] }}</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</template>
<script>
import Selection from '../components/base/selection'	
import DatePicker from '../components/base/datepicker'	
import _ from 'lodash'	
export default{
	components:{
		Selection,
		DatePicker
	},
	data(){
		return {
			productId:0,
			startDate:'',
			endDate:'',
			query:'',
			currentOrder:'asc',
			orderList:[],
			products:[
				{
					label:'数据统计',
					value:0
				},
				{
					label:'数据预测',
					value:1
				},
				{
					label:'流量分析',
					value:2
				},
				{
					label:'广告发布',
					value:3
				}
			],
			headList:[
				{
					label:'订单号',
					value:0,
					name:'orderId',
					active:false
				},
				{
					label:'购买产品',
					value:1,
					name:'product',
					active:false
				},
				{
					label:'版本类型',
					value:2,
					name:'version',
					active:false
				},
				{
					label:'有效时间',
					value:3,
					name:'period',
					active:false
				},
				{
					label:'购买日期',
					value:4,
					name:'date',
					active:false
				},
				{
					label:'数量',
					value:5,
					name:'buyNum',
					active:false
				},
				{
					label:'总价',
					value:0,
					name:'amount',
					active:false
				}

			]
		}
	},
	watch:{
		query(){
			this.getOrderList();
		}
	},
	methods:{
		getOrderList(){
			let reqParams = {
				query:this.query,
				productId:this.productId,
				startDate:this.startDate,
				endDate:this.endDate
			}

			this.$http.get('../static/db.json').then((res) => {
					this.orderList = res.data.getOrderList.list;
				},(error) => {
					console.log(error);
				})

		},
		changeOrderType(headItem){
			this.headList.map((item) => {
				item.active = false;
				return item;
			});
			headItem.active = true;
			if(this.currentOrder === 'asc'){
				this.currentOrder = 'desc';
			}
			else if(this.currentOrder === 'desc')
			{
				this.currentOrder = 'asc';
			}
			this.orderList = _.orderBy(this.orderList,headItem.name,this.currentOrder);
		},
		changeProductId(obj){
			this.productId = obj.value;
			this.getOrderList();
		},
		changeStartDate(date){
			this.startDate = date;
			this.getOrderList();
		},
		changeEndDate(date){
			this.endDate = date;
			this.getOrderList();
		}	
	},
	mounted(){
		this.getOrderList();
	},
}
</script>
<style>
.orderList{
	width:1200px;
	min-height:800px;
	margin-top:20px auto;
	overflow: hidden;
}
.orderList h3{
	font-size: 20px;
	font-weight: bold;
	margin:20px 0;
}
.order-list-option{
	display: inline-block;
	padding-left:15px;
}
.order-list-option:nth-child(1){
	padding-left:0;
}
.order-list-table table{
	width:100%;
	margin:30px 0;

}
.order-list-table th,
.order-list-table td{
	height:30px;
	line-height: 30px;
	text-align: center;
}
.order-list-table td{
	border:1px solid #e3e3e3;
	background: #fff;
}
.order-list-table th{
	border:1px solid #4fc08d;
	background:#4fc08d;
	color:#fff;
	font-weight: bold;
	cursor: pointer;
}
.order-list-table th.active{
	background: blue;
}
.query{
	height:25px;
	line-height: 25px;
	border:1px solid #e3e3e3;
	text-indent: 10px;
}
</style>