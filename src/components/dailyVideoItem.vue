<template>
    <view>
        <view class="videolist-header">
            <view class="videolist-header-icon">
                <img :src="item.data.content.data.provider.icon" alt="">
            </view>
            <view class="videolist-header-name">
                {{item.data.content.data.provider.name}}
            </view>
            <view class="videolist-header-more" @click="clickMore">
                <image src="../static/more.png"></image>
            </view>  
        </view>
        
        <view class="videolist-tags">
            <view>
                <text class="videolist-littletag tag-normal" v-for="tag in item.data.content.data.tags" :key="tag.id">
                    #{{tag.name}}#
                </text>
                <text class="videolist-littletag tag-black">
                    {{item.data.content.data.title}}
                </text>
            </view>
        </view>

        <view class="videolist-content" @click="setVideoStorage()">
            <view class="videolist-content-image">
                <image :src="item.data.content.data.cover.detail" alt="" mode="widthFix"></image>
            </view>
            <view class="videolist-content-dura">
                {{time}}
            </view>
        </view>

        <view class="videolist-footer">
            <view class="videolist-footer-title">
                {{item.data.content.data.description}}  
            </view>
        </view>
    </view>
</template>

<script>
export default {
    data(){
        return {
            time: ''
        }
    },
    props: ['item'],
    onReady(){
        const time = this.item.data.content.data.duration
        if (time >= 60) {
            let s = time % 60;
            let m = parseInt(time / 60);
            if(s < 10){
                s = '0' + s;
            }
            if(m < 10){
                m = '0' + m;
            }
            this.time = m + ':' + s;
        }
    },
    methods: {
        setVideoStorage(){
            uni.setStorage({
                key: "videoItem_key",
                data: this.item,
                success(){
                    // console.log('set success');
                    uni.navigateTo({
                        url: "../video/video"
                    })
                }
            })
        },
		getList(arr,data){
			let newArr = arr;
			if(arr.length == 0){
				arr.push(data)
				uni.showToast({
					title: '添加成功'
				})
			} else {
				let cArr = arr.map(item => item.id);
				let result = cArr.indexOf(data.id);
				if(result === -1){
					arr.push(data);
					uni.showToast({
						title: '添加成功'
					})
				} else {
					uni.showToast({
						title: '您已添加此视频',
						icon: "none"
					})
				}
			}
			newArr = arr;
		},
        clickMore(){
			let that = this;
            uni.showActionSheet({
                itemList: ['★分享★', '★收藏★', '稍后观看'],
                success: function (res) {
                    switch (res.tapIndex) {
                        case 0:
                            uni.showToast({
                            	title: '暂未开放',
								icon: "none"
                            })
                            break;
                        case 1:
							that.getList(getApp().globalData.collectionList,that.item);
                            break;
                        case 2:
							that.getList(getApp().globalData.watchLaterList,that.item);
                            break;
                    }
                }
            });
        }
    }
}
</script>

<style>
    .videolist-header{
        display: flex;
        flex-direction: row;
        margin-top: 5px;
    }
    .videolist-header-name{
        height: 65upx;
        line-height: 65upx;
        padding: 0 20upx;
        flex: 1;
    }
    .videolist-header-icon{
        border: 1px solid #ccc;
        border-radius: 10px;
    }
    .videolist-header-icon img{
        display: block;
        width: 75upx;
        height: 65upx;
        border-radius: 10px;
    }
    .videolist-header-more image{
        height: 65upx;
        width: 65upx;
        display: block;
    }

    .videolist-littletag{
        font-size: 26upx;
        color: blue;
        padding: 0 4upx;
		margin-right: 2upx;
    }
	.tag-normal{
		display: inline-block;
		background: #F6F6F6;
		border-radius: 10upx;
	}
    .tag-black{
        color: #000;
    }

    .videolist-content{
        position: relative;
    }
    .videolist-content-image{
		margin-top: 10upx;
        width: 100%;
    }
    .videolist-content-image image{
        display: block;
        width: 100%;
        border-radius: 5px;
    }
    .videolist-content-dura{
        position: absolute;
        bottom: 30upx;
        left: 50upx;
        background: rgba(189, 189, 189,.5);
        color: #fff;
        font-size: 24upx;
        padding: 0 5px;
        border-radius: 5px;
    }

    .videolist-footer{
        border-bottom: 1px solid #ccc;
        border-radius: 10px;
        padding-bottom: 20upx;
    }
    .videolist-footer-title{
        font-size: 28upx;
        padding: 3px 0;
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
        word-wrap: break-word;
        white-space: normal;
        -webkit-line-clamp: 1;
        -webkit-box-orient: vertical;
    }
    
</style>

