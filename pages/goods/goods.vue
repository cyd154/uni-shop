<template>
	<view class="goods">
		<goods-list :goods='goods' />
		<view class="isOver" v-if="flag">
			————————到底了————————
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list'
	
	export default {
		components:{
			goodsList
		},
		data() {
			return {
				goods:[],
				pagenum:1,
				flag:false,
				goodsTotal:0
			}
		},
		methods: {
			async getgoods () {
				const res = await this.$http({
					url:'/goods/search',
					data:{
						pagenum: this.pagenum
					}
				})
				this.goods = [...this.goods,...res.data.message.goods]
				this.goodsTotal = res.data.message.total
				// console.log(this.goodsTotal)
				
			}
		},
		onLoad() {
			this.getgoods()
		},
		onReachBottom() {
			if(this.goods.length == this.goodsTotal){
				this.flag = true
			}else{
				this.pagenum++
				this.getgoods()
			}
		},
		onPullDownRefresh() {
			// console.log('xia')
			this.pagenum = 1
			this.goods = []
			this.flag = false
			this.getgoods()
			uni.stopPullDownRefresh()
		}
		
	}
</script>

<style>
.goods{
	background-color: #eee;
	padding-top: 15rpx;
}
.isOver{
	width: 100%;
	height: 50px;
	line-height: 50px;
	text-align: center;
	font-size: 28rpx;
}
</style>
