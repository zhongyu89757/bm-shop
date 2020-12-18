<template>
	<view class="contact">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone()">联系电话：15846555816 (点击拨打)</view>
			<view>联系地址:中国云谷A7栋</view>
		</view>
		<map class="map" :longitude="longitude" :scale="scale" show_compass="true" :latitude="latitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:126.64469,
				latitude:45.635191,
				scale:15,			
				markers:[
					{
						id:1,
						latitude:45.635191,
						longitude:126.64469,
						title:"中国云谷",
						iconPath:"../../static/hmlogo.png",
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			//拨打电话
			phone(){
				uni.makePhoneCall({
				    phoneNumber: '15846555816' 
				});
			}
		}
	}
</script>

<style lang="scss">
	.contact{
		.img{
				height: 320rpx;
				width: 750rpx;
			}
		view{
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
		}
		
		.info{
				padding: 10rpx 20rpx;
				font-size: 30rpx;
		}
		map{
			width: 750rpx;
			height: 750rpx;
		}
	}

</style>
