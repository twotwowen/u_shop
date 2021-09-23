<template>
	<view class="goods">
		<good-list :goods="goods"></good-list>
		<view class="isOver" v-if="flag">
			-----我是有底线的-----
		</view>
	</view>
</template>

<script>
	import GoodList from '../../components/goodList/GoodList.vue'
	export default {
		name:'goods',
		components: {
			GoodList
		},
		data () {
			return {
				goods:[],
				page:1,
				flag:false
			}
		},
		onLoad() {
			this.getGoodList()
		},
		onReachBottom() {
			if(this.goods.length<this.page*10) return this.flag = true
			console.log('触底了')
			this.page++
			console.log(this.page)
			this.getGoodList()
		},
		onPullDownRefresh() {
			console.log('下拉刷新了')
			this.page=1
			this.goods = []
			this.flag = false
			setTimeout(() => {
				this.getGoodList(() => {
					uni.stopPullDownRefresh()
				})
			},500)
		},
		methods:{
			//获取商品列表
			async getGoodList(callback) {
				const res =await this.$myRequest({
					url:'/api/getgoods?pageindex='+this.page
				})
				this.goods = [...this.goods,...res.data.message]
				callback && callback()
			}
		}
	}
</script>

<style>
	.goodlist {
		background-color: #eee;
	}
	.isOver {
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
		background-color: #eee;
	}
</style>
