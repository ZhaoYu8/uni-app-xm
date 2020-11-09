<template>
	<view class="index">
		<u-navbar :is-back="false" title=" " :background="background">
			<u-search :show-action="false" class="search-wrap" placeholder="百种商品任你挑选"></u-search>
		</u-navbar>
		<view class="content">
			<view class="wrap">
				<u-swiper bg-color="#eeeeff" :list="list" interval="5000" :effect3d="true"></u-swiper>
			</view>
			<u-grid :col="4" :border="false" align="center">
				<u-grid-item v-for="item in arr" :key="item.image_url">
					<u-image width="100rpx" mode="aspectFit" height="100rpx" :src="item.image_url"></u-image>
					<view class="grid-text">{{item.description}}</view>
				</u-grid-item>
			</u-grid>
			<u-card margin="20rpx" class="card" :show-head="false" :show-foot="false" box-shadow="0 0 10rpx 0 #star">
				<view slot="body">
					<view class="u-flex u-row-between">
						<u-icon label=" " size="160" name="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-hobv75ysc5dp5010fc/96d59ba0-0f6f-11eb-b997-9918a5dda011.png"></u-icon>
						<view>欢迎你，我们竭诚为你服务！</view>
						<view class="u-flex">
							<u-icon label=" " size="40" name="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-hobv75ysc5dp5010fc/9837c3b0-0f6f-11eb-b244-a9f5e5565f30.png"
							 @click="makePhone"></u-icon>
							<button type="primary" open-type="contact" :show-message-card="true" plain class="icon-button">
								<u-icon label=" " size="40" name="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-hobv75ysc5dp5010fc/9cc980d0-0f6f-11eb-b244-a9f5e5565f30.png"></u-icon>
							</button>
						</view>
					</view>
				</view>
			</u-card>
			<headers />
		</view>
	</view>
</template>

<script>
	import headers from '../../components/header/header.vue'
	export default {
		data() {
			return {
				arr: [],
				list: [],
				background: {
					backgroundColor: '#001f3f',
					// 导航栏背景图
					background: 'url(https://cdn.uviewui.com/uview/swiper/1.jpg) no-repeat',
					// 还可以设置背景图size属性
					backgroundSize: 'cover',

					// 渐变色
					backgroundImage: 'linear-gradient(45deg, rgb(28, 187, 180), rgb(141, 198, 63))'
				}
			}
		},
		onLoad() {

		},
		components: {
			headers
		},
		mounted() {
			this.init();
		},
		methods: {
			async queryBanner() {
				let res = await uniCloud.callFunction({
					name: 'queryBanner'
				});
				let arr = res.result.data;
				arr = arr.sort(r => r.sort);
				this.list = arr.map(r => {
					return {
						r,
						...{
							image: r.image_url
						}
					}
				});
			},
			async querySortBanner() {
				let res = await uniCloud.callFunction({
					name: 'querySortBanner'
				});
				let arr = res.result.data;
				console.log(arr)
				arr = arr.sort(r => r.sort);
				arr.push({
					image_url: 'https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-hobv75ysc5dp5010fc/9c3a3920-0f6f-11eb-b680-7980c8a877b8.png',
					description: '更多'
				});
				this.arr = arr;
			},
			async init() {
				this.queryBanner();
				this.querySortBanner();
			},
			makePhone() {
				uni.makePhoneCall({
					phoneNumber: '13370229059'
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.index {
		overflow: hidden;
		background-color: #f5f5f5;

		.search-wrap {
			padding: 0 20rpx;
			flex: 1;
		}

		.wrap {
			padding: 20rpx;
		}

		.icon-button {
			display: flex;
			align-items: center;
			border: 0;
			padding: 0;
		}
	}
</style>
