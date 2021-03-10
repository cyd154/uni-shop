<template>
	<view class="home">
		<swiper :indicator-dots="true" :circular="true">
			<swiper-item v-for="item in swiper" :key="item.goods_id">
				<image :src="item.image_src"></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in nav" :key="index" @click="tonav(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.tit}}</text>
			</view>
		</view>
		<!-- 推荐商品区域 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list @navigator="goGoodsDetail" :goods='goods' />  
		</view>
		<view class="isOver" v-if="flag">
			————————到底了————————
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list'
	
	export default {
		name:'home',
		components:{
			goodsList
		},
		data() {
			return {
				swiper:[],
				goods:[],
				pagenum: 1,
				flag:false,
				nav:[
					{
						icon:'iconfont icon-ziyuan',
						tit:'商品',
						path:'../goods/goods'
					},
					{
						icon:'iconfont icon-tupian',
						tit:'分类',
						path:'../pics/pics'
					},
					{
						icon:'iconfont icon-shipin',
						tit:'视频',
					},
					{
						icon:'iconfont icon-guanyuwomen',
						tit:'联系',
						path:'../contact/contact'
					},
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		methods: {
			// 获取轮播图数据
			async getSwipers() {
				const res = await this.$http({
					url:'/home/swiperdata'
				})
				// console.log(res)
				this.swiper = res.data.message
			},
			// 获取商品列表
			async getHotGoods() {
				const res = await this.$http({
					url:'/goods/search',
					data:{
						pagenum: this.pagenum
					}
				})
				// console.log(res)
				this.goods = [...this.goods,...res.data.message.goods]
			},
			tonav(url) {
				uni.navigateTo({
					url
				})
			},
			onReachBottom() {
				if(this.goods.length<this.pagenum*10) return this.flag = true
				this.pagenum++
				this.getHotGoods()
			},
			onPullDownRefresh() {
				// console.log('xia')
				this.pagenum = 1
				this.goods = []
				this.flag = false
				this.getHotGoods()
				uni.stopPullDownRefresh()
			},
			goGoodsDetail(id) {
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
				
			}
		}
	}
</script>

<style lang="scss">
.home{
	swiper{
		width: 750rpx;
		height: 380rpx;
		image{
			width: 100%;
			height: 100%;
		}
	}
	.nav{
		display: flex;
		.nav_item{
			width: 25%;
			text-align: center;
			view{
				width: 120rpx;
				height: 120rpx;
				background-color: $shop-color;
				border-radius: 60rpx;
				margin: 10px auto;
				line-height: 120rpx;
				color: #fff;
				font-size: 50rpx;
			}
			text{
				font-size: 30rpx;
			}
		}
	}
	.hot_goods{
		background-color: #eee;
		overflow: hidden;
		margin-top: 10px;
		.tit{
			height: 50px;
			line-height: 50px;
			color: $shop-color;
			text-align: center;
			letter-spacing: 20px;
			background-color: #fff;
			margin: 15rpx 0;
		}
	}
}
</style>
