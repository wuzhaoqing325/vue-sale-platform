<template>
	<div class="login-form">
		<!-- 用户名 -->
		<div class="login-form-line">
			<div class="login-form-line-left">
				用户名：
			</div>
			<div class="login-form-line-right">
				<input type="text" placeholder="请输入用户名" v-model="username">
				<span class="error">{{usernameErr.errorText}}</span>
			</div>
		</div>
		<!-- 密码 -->
		<div class="login-form-line">
			<div class="login-form-line-left">
				密码：
			</div>
			<div class="login-form-line-right">
				<input type="password" placeholder="请输入密码" v-model="password">
				<span class="error">{{passwordErr.errorText}}</span>
			</div>
		</div>
		<!-- 登录按钮 -->
		<div class="login-form-line">
			<div class="login-form-btn button" @click="showWarning">
				注册
			</div>
		</div>
		<p class="warning" v-if="isShowWarning">部分选项未通过</p>
	</div>
</template>
<script>
export default{
	data(){
		return {
			errorText:'abc',
			password:'',
			username:'',
			usernameFlag:false,
			passwordFlag:false,
			isShowWarning:false
		}
	},
	computed:{
		usernameErr(){
			let errorText,status;
			if(!/@/g.test(this.username)){
				errorText = '不包含@';
				status = false;
			}
			else{
				errorText = '';
				status = true;
			}
			if(!this.usernameFlag){
				errorText = '';
				this.usernameFlag = true;
			}
			return {
				errorText,
				status
			}
		},
		passwordErr(){
			let errorText,status;
			if(!/^\w{1,6}$/g.test(this.password)){
				errorText = '不是1-6位密码';
				status = false;
			}
			else{
				errorText = '';
				status = true;
			}
			if(!this.passwordFlag){
				errorText = '';
				this.passwordFlag = true;
			}
			return {
				errorText,
				status
			}
		}
	},
	methods:{
		showWarning(){
			if(this.usernameErr.status !==true || this.passwordErr.status !==true){
				this.isShowWarning = true;
			}
		}
	}
}
</script>
