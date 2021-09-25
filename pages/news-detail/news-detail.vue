<template>
	<view class="news_detail">
			<text class="title">
				<h2>{{newsdetail.title}}</h2>
			</text>
			<view class="info">
				<text>发表时间：{{formatDate(newsdetail.add_time)}}</text>
				<text>浏览：{{newsdetail.click}}</text>
			</view>
			<view class="content">
				<rich-text :nodes="newsdetail.content"></rich-text>
			</view>
		</view>
</template>

<script>
	export default {
		data() {
			return {
				id:14,
				newsdetail:{},
				}
		},
		onLoad(options) {
			this.id = options.id
			this.getnewsdetail()
		},
		methods: {
			async getnewsdetail() {
				const res = await this.$myRequest({
					url:'/api/getnew/'+this.id
				})
				this.newsdetail = res.data.message[0]
				console.log(this.newsdetail)
			},
			formatDate(date) {
				const nDate = new Date(date)
				const year = nDate.getFullYear()
				const month = nDate.getMonth().toString().padStart(2,0)
				const day = nDate.getDay().toString().padStart(2,0)
				return year+'-'+month+'-'+day
			}
		}
	}
</script>

<style lang="scss">
	.news_detail{
		font-size: 30rpx;
		padding: 0 20rpx;
		.title{
			text-align: center;
			width: 710rpx;
			display: block;
			margin: 20rpx 0;
		}
		.info{
			display: flex;
			justify-content: space-between;
			border-bottom: 1px solid #ccc;
			margin: 10rpx;
			padding: 20rpx 0;
		}
		.content {
			margin-top: 20rpx;
		}
	}
</style>
