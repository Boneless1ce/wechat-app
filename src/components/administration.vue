<template>
	<div class="list">
		<div class="on" v-if="data.length">
			<div class="item" v-for="item in data" :key="item.id">
				<div class="item-img">
					<img :src="item.data.content.data.cover.detail" alt="" mode="widthFix">
				</div>
				<div class="item-content">
					<div class="item-title">
						{{item.data.content.data.title}}
					</div>
					<div class="item-author">
						作者:{{item.data.content.data.provider.name}}
					</div>
					<div class="remove">
						<div class="remove-png" @click.native="showList(item.id)">
							<img src="../static/more.png" alt="">
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="off" v-if="data.length === 0">
			{{info.nullTitle}}
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				data: '',
				show: false
			}
		},
		props:['info'],
		onReady() {
			var arr
			if(this.info.list == 'collectionList'){
				arr = getApp().globalData.collectionList;
			} else if(this.info.list == 'watchLaterList'){
				arr = getApp().globalData.watchLaterList;
			}
			this.data = arr;
		},
		methods:{
			showList(id){
				let that = this;
				uni.showActionSheet({
					itemList: ['移除该视频'],
					success: function (res) {
						if(res.tapIndex == 0){
							uni.showModal({
								title: '提示',
								content: '是否移除该视频',
								success: function (res) {
									if (res.confirm) {
										var arr;
										var index;
										if(that.info.list == 'collectionList'){
											arr = getApp().globalData.collectionList;
										} else if(that.info.list == 'watchLaterList'){
											arr = getApp().globalData.watchLaterList;
										}
										let cArr = arr.map(function(x){
											if(x.id === id){
												index = arr.indexOf(x);
											}
										})
										arr.splice(index,1);
									} else if (res.cancel) {
										// console.log('用户点击取消');
									}
								}
							});
						}
					}
				});
			}
		}
	}
</script>

<style scoped>
	.off{
		position: absolute;
		left: 0;
		right: 0;
		top: 50%;
		transform: translateY(-50%);
		text-align: center;
		font-size: 36upx;
		color: #CCCCCC;
	}
	
	.item{
		margin: 0 0 20upx;
		padding: 0 30upx;
		background: #fff;
		display: flex;
		flex-direction: row;
		justify-content: flex-start;
		align-items: center;
	}
	.item-content{
		margin-left: 8upx;
		flex: 1;
	}
	.item-img img{
		width: 248upx;
		height: 160upx;
	}
	.item-title{
		font-size: 28upx;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}
	.item-author{
		font-size: 22upx;
		color: #CCCCCC;
	}
	.remove{
		float: right;
	}
	.remove img{
		width: 40upx;
		height: 40upx;
	}
</style>
