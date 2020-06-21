<template>
	<view>
	</view>
</template>

<script>
	export default {
		onLoad(query) {
			this.id = query.id;
			this.getComments();
		},
		data() {
			return {
				id: "",
				page: 1,
				comments: []
			};
		},
		methods: {
			getComments() {
				uni.showToast({
					icon:"none",
					title:"因跨域问题，无法获取评论。"
				})
				uni.request({
					url: `https://hot-topic-comment-wrapper-ms.juejin.im/v1/comments/${this.id}?pageNum=${this.page}&pageSize=20`,
					header:{
						"X-Juejin-Src": "web",
					},
					success:(res)=>{
						this.comments.push(...res.data.d.comments);
					}
				})
			}
		}
	}
</script>

<style lang="scss">

</style>
