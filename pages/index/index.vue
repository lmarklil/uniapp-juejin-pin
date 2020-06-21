<template>
	<view class="pins">
		<Pin v-for="(pin,index) in pins" :key="pin.id" :pin="pin" />
		<view v-if="loading" class="pins-loading">加载中</view>
	</view>
</template>

<script>
	import Pin from "./components/pin.vue";

	export default {
		components: {
			Pin
		},
		data() {
			return {
				pins: [],
				loading: false,
				pageCursor: "",
				hasNextPage: false,
				topicId: "249431a8e4d85e459f6c29eb808e76d0"
			}
		},
		onLoad() {
			this.getPins();
		},
		onReachBottom() {
			if (this.hasNextPage) this.getPins(this.pageCursor);
		},
		methods: {
			getPins(cursor = "") {
				this.loading = true;
				uni.request({
					url: "https://web-api.juejin.im/query",
					method: "POST",
					header: {
						"X-Agent": "Juejin/Web"
					},
					data: {
						operationName: "",
						query: "",
						variables: {
							size: 20,
							after: cursor
						},
						extensions: {
							query: {
								id: this.topicId
							}
						}
					},
					success: (res) => {
						const data = res.data.data.recommendedActivityFeed;
						data.items.edges.forEach(item => this.pins.push(item.node.targets[0]));
						this.pageCursor = data.items.pageInfo.endCursor;
						this.hasNextPage = data.items.pageInfo.hasNextPage;
						this.loading = false;
					},
					fail: () => {
						uni.showToast({
							title: "数据获取失败"
						})
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.pins {
		background: #f5f5f5;

		&-loading {
			padding: 20rpx 0;
			color: #333;
			font-size: 20rpx;
			text-align: center;
		}
	}
</style>
