<template>
	<div class="checkOrder-component">
		<this-dialog :is-show="isShowCheckDialog" @on-close="checkStatus">
			<p>请检查您的支付状态!</p>
			<div class="button" @click="checkStatusSuccess">支付成功</div>
			<div class="button" @click="checkStatusFail">支付失败</div>
		</this-dialog>
		<this-dialog :is-show="isShowSuccessDialog" @on-close="toOrderList">
			<p>支付成功！</p>
		</this-dialog>
		<this-dialog :is-show="isShowFailDialog" @on-close="toOrderList">
			<p>支付失败！</p>
		</this-dialog>
	</div>
</template>
<script>
import ThisDialog from './base/dialog'
export default{
	components:{
		ThisDialog
	},
	props:{
		isShowCheckDialog:{
			type:Boolean,
			default:false
		},
		orderId:{
			type:[String,Number]
		}
	},
	data(){
		return {
			isShowSuccessDialog:false,
			isShowFailDialog:false
		}
	},
	methods:{
		checkStatus(){
			console.log(this.orderId);
			this.$emit('on-close-check-dialog');
		},
		checkStatusSuccess(){
			this.isShowSuccessDialog = true;
			this.$emit('on-close-check-dialog');
		},
		checkStatusFail(){
			this.isShowFailDialog = true;
			this.$emit('on-close-check-dialog');
		},
		toOrderList(){
			this.isShowSuccessDialog = false;
			this.isShowFailDialog = false;
			this.$emit('on-close-check-dialog');
			this.$router.push({path:'/orderList'})
		}
	}
}
</script>
<style>
.checkOrder-component p{
	display: inline-block;
	margin-right:10px;
}
</style>