<template>
	<view class="pics">
		<scroll-view scroll-y="true" class="left">
			<view 
			@click="leftClickHandle(index,item.id)"
			:class="active===index ? 'active' : ''"
			v-for="(item,index) in cates" 
			:key="item.id">{{item.title}}</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="right">
			<view 
			v-for="(item,index) in secondData" 
			:key="index">
			<image :src="item.imgurl" @click="imgClick(item.imgurl)"></image>
			<text>{{item.title}}</text>
			</view>
			<!-- <text v-if="secondData.length === 0">暂无数据</text> -->
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:0,
				secondData:[],
				img:[]
			}
		},
		onLoad() {
			this.getPicsCates(),
			this.leftClickHandle()
		},
		methods:{
			async getPicsCates() {
				const res = await this.$myRequest({
					url:'/api/getimgcategory',
				})
				// console.log(res)
				this.cates = res.data.message
			},
			async leftClickHandle (index=0,id) {
				this.active = index
				//获取右边的数据
				// const res =await this.$myRequest({
				// 	url:'/api/getimages/'+id
				// })
				// this.secondData = res.data.message
				await	uni.request({
					url:'https://api.muxiaoguo.cn/api/bing?id=today&pn=8',
					success: (res) => {
						
						console.log('获取图片成功')
						this.secondData = res.data.data
						
					},
					fail: (err) => {
						uni.showToast({
							title:'获取图片失败',
							icon:'error'
							
						})
					}
				})
			},
			//完成图片预览功能
			imgClick(current) {
				const urls = this.secondData.map(item => {
					return item.imgurl
				})
				uni.previewImage({
					current,
					urls
				})
			}
		}
		
	}
</script>

<style lang="scss">
	page {
		height: 100%;
	}
	.pics {
		height: 100%;
		display: flex;
		.left {
			height: 100%;
			width: 220rpx;
			border-right: 1px solid #eee;
			view {
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}
			.active {
				background: $shop-color;
				color: #fff;
			}
		}
		.right {
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;
			.item{
				image{
					width: 520rpx;
					height: 520rpx;
					border-radius: 5px;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	
	}
</style>
