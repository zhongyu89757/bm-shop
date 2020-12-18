<template>
		<view class="home">
			<swiper indicator-dots circular>
				<swiper-item v-for="item in swipers" :key="item.id">
					<image  :src="item.img"></image>
				</swiper-item>
			</swiper>
			<!-- 导航区 -->
			<view class="nav">
				<view class="nav_item" v-for="item in navs" :key="item.id" @click="navItemClick(item.path)">
					<view :class="item.icon"></view>
					<text>{{item.title}}</text>					
				</view>				
			</view>
			<!-- 推荐商品 -->
			<view class="hot_goods">
				<view class="title">
					推荐商品
				</view>
				<goods_list :goods="goods"></goods_list>
			</view>
		</view>
</template>

<script>
	import goods_list from "../components/goods_list.vue"
	export default {
		data() {
			return {
				swipers:[],
				goods:[],
				navs: [
					{
						icon: 'iconfont icon-ziyuan',
						title: '黑马超市',
						path: '/pages/goods/goods',
						id:0
					},
					{
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact',
						id:1
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics',
						id:2
					},
					{
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos',
						id:3
					}
				]
			}
		},
		onLoad() {
			this.getSwipers();		
			this.getHotGoods();
		},
		methods: {
		//获取轮播图数据
			async getSwipers () {
					const res = await this.$myRequest({
						url: '/api/getlunbo'
					})
					this.swipers = res.data.message
					},
		//获取商品列表			
			async getHotGoods() {
					const res = await this.$myRequest({
						url: '/api/getgoods?pageindex=1'
					})
					this.goods = res.data.message
					},
				//点击导航处理函数
				 navItemClick(url){
						uni.navigateTo({
							url
						})		
					}
					
		},
		components:{
			goods_list
		}
	}
</script>

<style lang="scss">
	.home {
		swiper{
			width: 750rpx;
			height: 380rpx;
			image:{
				width: 100%;
				height: 100%;
			}
		}
		.nav {
			display:flex;
			
			.nav_item {
				width: 25%;
				text-align: center;
				view {
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60px;
					margin:10rpx auto;
					line-height: 120rpx;
					color: #FFFFFF;
					font-size: 50rpx;
				}
				.icon-tupian {
					font-size: 45rpx;
				}
				text:{
					font-size: 30rpx;
				}
				
			}
			
		}
		.hot_goods{
				background: #eee;
				overflow: hidden;
				.title{
					text-align: center;
					height: 45px;
					line-height: 45px;	
					color: $shop-color;
					background: #FFFFFF;
					letter-spacing: 20rpx;
					margin: 7rpx 0;
				}
		}
		
	}
	
	
	
	
</style>
