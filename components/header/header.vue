<template>
	<view class="recommend">
		<view class="box">
			<text class="licon licon1"></text>
			<text class="licon"></text>
			<view>{{text}}</view>
			<text class="ricon ricon1"></text>
			<text class="ricon"></text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		props: {
			text: {
				default: '精品推荐'
			}
		}
	}
</script>
<style lang="scss" scoped>
	.recommend {
		background-color: #fff;
		color: #000;
		font-size: 40rpx;
		display: flex;
		align-items: center;
		justify-content: center;

		.box {
			position: relative;
			display: flex;
			align-items: center;

			.licon {
				left: -40rpx;
				top: 50%;
				transform: rotate(30deg) translateY(-50%);
				position: absolute;
				height: 80%;
				width: 5rpx;
				background-color: #00beff;
				border-radius: 10rpx;
			}

			.licon1 {
				left: -55rpx;
				height: 50%;
				background-color: #af00ff;
			}

			.ricon {
				right: -20rpx;
				top: 50%;
				transform: rotate(30deg) translateY(-50%);
				position: absolute;
				height: 80%;
				width: 5rpx;
				background-color: #00beff;
				border-radius: 10rpx;
			}

			.ricon1 {
				right: -40rpx;
				height: 50%;
				background-color: #af00ff;
			}
		}
	}
</style>
