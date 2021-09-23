<template>
	<view class="contact">
		<image src="../../static/icon/about.jpg" mode=""></image>
		<view class="info">
		<view @click="phone">
		联系我们：123456789（点击拨打）
		</view>
		<view>
			地址：xxxxxxxxxxxxxxxxxxxxxxxx
		</view>
		</view>
		
		<map class="map"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				latitude:113.33237,
				longitude:23.15554
			}
		},
		methods: {
			phone() {
				uni.makePhoneCall({
					phoneNumber:'10086'
				})
			}
		}
	}
</script>

<style lang="scss">
.contact{
	image{
		width: 750rpx;
		height: 320rpx;
	}
	.info{
		padding: 10rpx 20rpx;
		font-size: 30rpx;
		view{
			line-height: 80rpx;
			border-bottom: 1px solid #eee;
		}
	}
	
	.map{
		width: 750rpx;
		height: 750rpx;
	}
}
</style>
