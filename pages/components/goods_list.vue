<template>
	<view class="goods_list" >
		<view class="goods_item" v-for="(item,index) in goods" :key="item.id">
			<image :src="item.img_url"></image>
			<view class="price">
				<text>{{item.sell_price}}</text>
				<text>{{item.market_price}}</text>
			</view>
			<view class="name">{{item.title}}</view>
		</view>			
	</view>
</template>

<script>
	export default{
		props:['goods']
	}
</script>

<style lang="scss">
	.goods_list {
		padding:0 7px;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.goods_item{
			background: #FFFFFF;
			width: 355rpx;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;
		}
		image{
			height: 150px;
			width: 80%;
			display: block;
			margin: auto;
		}
		.price{
			color: $shop-color;
			font-size: 36rpx;
			margin: 10rpx 0rpx 5rpx 0;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				margin-left: 10rpx;
				text-decoration: line-through;
				
			}
		}
		.name{
			font-size: 28rpx;
			line-height: 50rpx;
			padding-bottom: 15rpx;
			padding-top: 10rpx;
		}
		
	}
</style>
