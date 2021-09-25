<template>
	<view class="home">
		<!-- 轮播图 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" circular="true">
			<swiper-item v-for="(item) in swipers" :key=item.id>
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		
		<!-- 导航 -->
		<view class="navs">
			<view class="navs_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.text}}</text>
			</view>
		</view>
		
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="title">推荐商品</view>
			<good-list :goods="goods" @goodsDetail="goodsDetail"></good-list>
		</view>
	</view>
</template>

<script>
	import GoodList from '../../components/goodList/GoodList.vue'
	export default {
		components:{
			GoodList
		},
		data() {
			return {
				swipers:[],
				navs:[
					{
						icon:'iconfont icon-chaoshi',
						text:'又是超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-tupian',
						text:'社区图片',
						path:'/pages/pic/pic'
					},
					{
						icon:'iconfont icon-shipin',
						text:'学习视频',
						path:'/pages/video/video'
					},
					{
						icon:'iconfont icon-guanyu',
						text:'联系我们',
						path:'/pages/contact/contact'
					}
				],
				goods:[]
			}
		},
		onLoad() {
			this.getSwipers(),
			this.getGoodList()
			
		},
		methods: {
			//获取轮播图数据
			async getSwipers() {
				const res = await this.$myRequest({
					url:'/api/getlunbo'
				})
				this.swipers = res.data.message
			},
			
			//获取商品列表
			async getGoodList() {
				const res =await this.$myRequest({
					url:'/api/getgoods?pageindex=1'
				})
				this.goods = res.data.message
			},
			//跳转到商品列表
			navItemClick(path) {
				console.log('点击了'),
				uni.navigateTo({
					url:path
				})
			},
			goodsDetail(id) {
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
			}
			
		}
	}
</script>
	
<style lang="scss">
	.home {
		/*轮播图*/
		swiper {
			width: 750rpx;
			height: 380rpx;
			image {
				width: 100%;
				height: 100%;
			}
		}
		/*navs */
		.navs {
			display: flex;
			.navs_item {
				width: 25%;
				text-align: center;
				view { 
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60rpx;
					margin: 10px auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}
				text {
					font-size: 30rpx;
				}
			}
		}
		// 推荐商品
		.hot_goods {
			background-color: #eee;
			overflow: hidden;
			margin-top: 10px;
			.title {
				color: $shop-color;
				text-align: center;
				height: 100rpx;
				line-height: 100rpx;
				letter-spacing: 20px;
				background-color: #fff;
				margin: 7rpx 0;
				font-weight: 600;
				
			}
		}
	}
</style>
