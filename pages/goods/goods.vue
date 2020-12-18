<template>
	<view class="goods_list">
		<goods_list :goods="goods"></goods_list>
		<view class="isOver" v-if="flag">-----我是有底线的-----</view>
	</view>
</template>

<script>
	import goods_list from "../components/goods_list.vue"
	export default {
		data() {
			return {
				goods:[],
				pageindex: 1,
				flag :false
			}
		},
		onLoad() {
				this.getGoodsList()
		},
		//下拉刷新
		onPullDownRefresh() {
			this.pageindex=1;
			this.goods=[];
			this.flag=false;
			setTimeout(()=>{
				this.getGoodsList(()=>{
					uni.stopPullDownRefresh()
				})
			},1000)
			
		},
		//向下拖拽
		onReachBottom() {
			console.log(this.goods.length)
			if(this.goods.length<this.pageindex*10) return this.flag=true	
			this.pageindex++
			this.getGoodsList();
		},
		methods: {
			//获取商品列表
				async getGoodsList(callBack) {
						const res = await this.$myRequest({
							url: '/api/getgoods??pageindex='+this.pageindex
						})
						this.goods =[...this.goods,...res.data.message]
						callBack && callBack()
						},
				
		},
		components:{
			goods_list
		}
	}
</script>

<style lang="scss">
	.goods_list {
			background: #eee;;
		}
		.isOver {
			width: 100%;
			height: 50px;
			line-height: 50px;
			text-align: center;
			// background: #fff;
			font-size: 28rpx;
		}
		.isOver{
			font-size: 28rpx;
			width: 100%;
			height: 50px;
			text-align: center;
			line-height: 50px;
		}

</style>
