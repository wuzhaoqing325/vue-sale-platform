<template>	
		<div class="index">
			<div class="index-left">
				<!-- 上面的全部样品 -->
				<div class="index-left-products">
				<h2>全部产品</h2>
				<template v-for="product in products">
					<div class="index-left-title">{{ product.title }}</div>
					<ul class="index-left-list">
						<li v-for="item in product.list">
							<a :href="item.herf">{{ item.label }}</a>
							<span v-if="item.hot" class="hot-tag">HOT</span>
						</li>
					</ul>
					<div class="hr" v-if="!product.last"></div>
				</template>
				</div>
				<!-- 下面的最新消息	 -->
				<div class="index-left-news">
					<h2>最新消息</h2>
					<ul>
						<li v-for="news in newsList">
							<a :href="news.url">{{ news.title }}</a>
						</li>
					</ul>
				</div>
			</div>
			<div class="index-right">
				<!-- 上面的轮播图部分 -->
				<slide-show :slides="slidesList" :inv="invTime"></slide-show>
				<!-- 下面的广告部分 -->
				<div class="board">
					<ul>
						<li v-for="(board,index) in boardList"
						:class="{'line-last': index% 2!== 0}">
							<div class="board-img" :class="board.id">
								</div>
							<div class="board-text">
								<h3>{{ board.title }}</h3>
							<p>{{ board.description }}</p>
							<router-link :to="{path:'detail/'+board.toKey}">
								<div class="button">立即购买</div>
							</router-link>
							</div>
						</li>
					</ul>
				</div>
			</div>
		</div>
</template>
<script>
import	SlideShow from '../components/slideShow'
export default{
	components:{
		SlideShow
	},
	created: function () {
    this.$http.get('../static/db.json')
    .then((res) => {
      this.newsList = res.data.getNewsList;
      // console.log(this.newsList)
    }, (err) => {
      console.log(err)
    })
  },
	data(){
		return {
			invTime:2000,
			slidesList:[
				{
					title:'第1张图片',
					src:require('../assets/slideShow/pic1.jpg')
				},
				{
					title:'第2张图片',
					src:require('../assets/slideShow/pic2.jpg')
				},
				{
					title:'第3张图片',
					src:require('../assets/slideShow/pic3.jpg')
				},
				{
					title:'第4张图片',
					src:require('../assets/slideShow/pic4.jpg')
				}

			],
			newsList:[],
			products:{
				pc:{
					title:'PC产品',
					list:[
						{
							label:'数据统计',
							value:0,
							herf:'https://www.baidu.com/'
						},
						{
							label:'数据预测',
							value:1,
							herf:'https://www.baidu.com/'
						},
						{
							label:'流量分析',
							value:2,
							hot:true,
							herf:'https://www.baidu.com/'
						},
						{
							label:'广告发布',
							value:3,
							herf:'https://www.baidu.com/'
						}
					]
				},
				app:{
					title:'手机应用类',
					last:true,
					list:[
						{
							label:'91助手',
							value:0,
							herf:'https://www.baidu.com/'
						},
						{
							label:'产品助手',
							value:1,
							hot:true,
							herf:'https://www.baidu.com/'
						},
						{
							label:'智能地图',
							value:2,
							herf:'https://www.baidu.com/'
						},
						{
							label:'团队语音',
							value:0,
							herf:'https://www.baidu.com/'
						}
					]
				}

			},
			boardList:[
				{
					title:"开放产品",
					description:"开放产品是一款开放产品",
					id:'earth',
					toKey:'count'
				},
				{
					title:"品牌营销",
					description:"品牌营销帮助你的产品更好地找到定位",
					id:'loud',
					toKey:'forecast'
				},
				{
					title:"使命必达",
					description:"使命必达快递迭代永远保持最前端的速度",
					id:'car',
					toKey:'analysis'
				},
				{
					title:"勇攀高峰",
					description:"帮你勇闯高峰，到达事业的顶峰",
					id:'hill',
					toKey:'publish'
				}
			]
		}
	}
}
</script>
<style>
.index{
	overflow: hidden;
}
.index-left{
	width:280px;
	float:left;
	
	margin-top:15px;
}
.index-right{
	width:900px;
	float:right;
	
	margin-top:15px;
}
.index-left-products{
	overflow: hidden;
	background: #fff;
}
.index-left h2{
	height:35px;
	line-height: 35px;
	background:#4fc08d;
	color:#fff;
	font-size:14px;
	font-weight:bold;
	padding-left:15px;
}
.index-left-title{
	margin:20px 0;
	padding-left:15px;
	font-weight:bold;
}
.index-left-list{
	padding-left:15px;
}
.index-left-list li{
	padding-left:5px;
	margin-bottom:15px;
}
a{
	text-decoration: none;
	color:#000;
}
.index-left-list li:hover{
	cursor: pointer;
}
.hot-tag{
	background:red;
	color:#fff;
}
.hr{
	width:100%;
	height:1px;
	background: #aaa;
}
.index-left-news{
	margin-top:15px;
	background: #fff;
	min-height: 465px;
}
.index-left-news ul{
	padding-left:15px;
	padding-top:15px;
}
.index-left-news ul li{
	width:230px;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	margin-bottom:15px;
	cursor: pointer;
}
.board{
	overflow: hidden;
	margin-top:15px;
}
.board ul li{
	width:440px;
	float:left;
	margin-right:20px;
	background: #fff;
	margin-bottom:20px;
	height:160px;


}

.board ul li.line-last{
	margin-right:0;
}
.board-img.car,
.board-img.loud,
.board-img.earth,
.board-img.hill{
	display: inline-block;
	width:100px;
	height:100px;
	margin-top:30px;
	margin-left:20px;
	float:left;
}

.board-img.car{
		
	background: url('../assets/images/2.png') no-repeat;
}
.board-img.earth{
	background: url('../assets/images/1.png') no-repeat;
}
.board-img.loud{
	background: url('../assets/images/3.png') no-repeat;
}
.board-img.hill{
	background: url('../assets/images/4.png') no-repeat;
}
.board-text{
	display: inline-block;
	padding-left:30px;
	padding-top:20px;	
}
.board-text h3{
	font-size: 22px;
	font-weight: bold;
}
.board-text p{
	
	margin:15px 0;
}
</style>