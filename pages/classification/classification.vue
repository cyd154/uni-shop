<template>
	<view class="goods">
		<goods-list @navigator="goGoodsDetail" :goods='goods' />
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
				goodsTotal:0,
				goodsId:0
			}
		},
		methods: {
			async getgoods () {
				const res = await this.$http({
					url:'/goods/search',
					data:{
						pagenum: this.pagenum,
						cid: this.goodsId
					}
				})
				// console.log(res)
				this.goods = [...this.goods,...res.data.message.goods]
				this.goodsTotal = res.data.message.total
				// console.log(this.goods)
			},
			goGoodsDetail(id) {
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
			}
		},
		onLoad(op) {
			this.goodsId = op.id
			this.getgoods()
		},
		onReachBottom() {
			if(this.goods.length == this.goodsTotal){
				this.flag = true
			}else{
				this.pagenum++
				this.getgoods()
			}
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
