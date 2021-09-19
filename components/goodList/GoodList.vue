<template>
	<view class="goodlist">
		<view class="goodlist_item" v-for="(item,index) in goods" :key="index">
			<image src="../../static/icon/sj.jpg"></image>
			<view class="price">
				<text>￥{{item.sell_price}}</text>
				<text>￥{{item.market_price}}</text>
			</view>
			<view class="tit">
				{{item.title}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:'GoodList',
		props:['goods'],
		
		data() {
			return {
				img:[]
			}
		}
		
	}
</script>

<style lang="scss">
	.goodlist {
		display: flex;
		width: 750rpx;
		flex-wrap: wrap;
		justify-content: space-around;
		.goodlist_item {
			width: 48%;
			background-color: #fff;
			margin: 10rpx 0;
			box-sizing:border-box;
			image {
				width: 80%;
				height:150px;
				display: block;
				margin: auto;
			}
			.price {
				color: $shop-color;
				font-weight: 36rpx;
				margin: 20rpx 0 5rpx 0;
				text:nth-child(2) {
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}
			.tit {
							font-size: 28rpx;
							line-height: 50rpx;
							padding-bottom: 15rpx;
							padding-top: 10rpx;
						}
		}
	}
</style>
