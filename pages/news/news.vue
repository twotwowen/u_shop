<template>
	<view class="news">
		<news-item :newslist="news" @itemClick="itemClick"></news-item>
	</view>
</template>

<script>
	import newsItem from '../../components/news-item/news-item.vue'
	export default {
		data() {
			return {
				news:[]
			}
		},
		components:{
			newsItem
		},
		onLoad() {
			this.getnewslist()
		},
		methods:{
			async getnewslist() {
				const res = await this.$myRequest({
					url:'/api/getnewslist'
				})
				console.log(res)
				this.news = res.data.message
			},
			itemClick(id) {
				console.log('点击了')
				uni.navigateTo({
					url:'../news-detail/news-detail?id='+id
				})
			}
		}
	}
</script>

<style></style>
