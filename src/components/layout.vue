<template>
	<div>
		<div class="app-wrap">
			<div class="app-head">
				<div class="app-head-inner">
					<router-link :to="{path:'/'}">
						<img :src="logoSrc" >
					</router-link>
					<ul>
						<li v-if="username===''" @click="showLogDialog">登录</li>
						<li v-if="username===''">|</li>
						<li v-if="username===''" @click="showRegDialog">注册</li>
						<li v-if="username!==''">{{username}}</li>
						<li v-if="username!==''">|</li>
						<li v-if="username!==''" @click="exitLogin">退出</li>
						<li>|</li>
						<li @click="showAboutDialog">关于</li>	
					</ul>
				</div>
			</div>
			<div class="app-content">
				<keep-alive>
					<router-view></router-view>
				</keep-alive>
			</div>
			<div class="app-foot">© 2019 fishenal MIT</div>
			<!-- 关于对话框 -->
			<my-dialog :is-show="isShowAboutDialog" @on-close="hideAboutDialog">
				<p>本报告在调研数据的基础上，采用定性与定量相结合的方式深入分析了专车市场发展的驱动因素与阻碍因素、专车市场背后的产业格局、专车企业的竞争格局、用户对专车市场的依赖程度、专车对其他交通工具运力的补充效应等，通过这五个章节的研究反映专车市场的发展态势和面临的问题。报告力求客观、深入、准确地反映中国专车市场发展情况，为政府、企事业单位和社会各界提供决策依据。</p>
			</my-dialog>
			<!-- 登录对话框 -->
			<my-dialog :is-show="isShowLogDialog" @on-close="hideLogDialog">
				<log-form @has-log="onSuccessLog"></log-form>
			</my-dialog>
			<!-- 注册对话框 -->
			<my-dialog :is-show="isShowRegDialog" @on-close="hideRegDialog">
				<reg-form></reg-form>
			</my-dialog>
		</div>
	</div>
</template>
<script>
import	MyDialog from './base/dialog'
import	LogForm from './logForm'
import	RegForm from './regForm'
export default{
	components:{
		MyDialog,
		LogForm,
		RegForm
	},
	data(){
		return{
			isShowAboutDialog:false,
			isShowLogDialog:false,
			isShowRegDialog:false,
			username:'',
			logoSrc:require('../assets/logo.png')
		}
	},
	methods:{
		showAboutDialog(){
			this.isShowAboutDialog = true;
		},
		hideAboutDialog(){
			this.isShowAboutDialog = false;
		},
		showLogDialog(){
			this.isShowLogDialog = true;
		},
		hideLogDialog(){
			this.isShowLogDialog = false;
		},
		showRegDialog(){
			this.isShowRegDialog = true;
		},
		hideRegDialog(){
			this.isShowRegDialog = false;
		},
		onSuccessLog(data){
			this.hideLogDialog();
			this.username = data.username;
		},
		exitLogin(){
			this.username = '';
		}

	}
}
</script>
<style>
	/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}


.app-wrap{
	width:100%;
	height:100%;
	background:#f3f3f3;
}
.app-head{
	width:100%;
	height:80px;
	background:#444;	
}
.app-head-inner{
	width:1200px;
	height:80px;
	margin:0 auto;
	line-height: 80px;
	vertical-align: middle;
	overflow: hidden;
}
.app-head-inner img{
	display: inline-block;
	margin-top:15px;
	width:50px;
}
.app-head-inner ul{
	display: inline-block;
	color:#fff;
	float:right;
}
.app-head-inner ul li{
	display: inline-block;
	padding-left:5px;
	cursor:pointer;
}
.app-foot{
	width:100%;
	height:100px;
	background:#e3e3e3;
	line-height: 100px;
	text-align:center;
}
.app-content{
	width:1200px;
	margin:0 auto;
	font-size:14px;
}
.button{
	padding:10px 15px;
	background: #4fc08d;
	color:#fff;
	cursor:pointer;
	display: inline-block;
}
/*登录注册对话框*/
.login-form-line{
	margin:20px;
	height:40px;
	line-height: 40px;

}
.login-form-line-left,
.login-form-line-right{
	display: inline-block;

}
.login-form-line-left{
	width:100px;
}
.login-form-line-right input {
	display: inline-block;
	width:250px;
	height:30px;
	border:1px solid #333;
	vertical-align: middle;
	padding-left:10px;	
}
.error{
	font-size: 14px;
	color:red;
}
.login-form-btn{
	height:20px;
	line-height: 20px;
	margin-left:150px;
}
.login-form p {
	color:red;
	margin-left:150px;
}

</style>