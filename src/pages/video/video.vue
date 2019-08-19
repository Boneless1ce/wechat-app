<template>
    <view>
        <view class="video-play">
            <video :src="videoPlay.playUrl" :poster="videoPlay.cover.detail"></video>
        </view>

        <view class="video-author">
            <image :src="videoPlay.author.icon"></image>
            <text>
                {{videoPlay.author.name}}
            </text>
            <!-- <view>
                关注
            </view> -->
        </view>

        <view class="video-content">
            <text class="video-description" @click="getHeight()">
                {{videoPlay.description}}
            </text>
            <view class="video-consumption">
                <text>
                    {{videoPlay.consumption.collectionCount}}收藏
                </text>
                <text>
                    {{videoPlay.consumption.replyCount}}留言
                </text>
                <text>
                    {{videoPlay.consumption.shareCount}}分享
                </text>
            </view>
            <text class="video-title">
                {{videoPlay.title}}
            </text>
        </view>

        <view class="video-tags">
            <text v-for="item in videoPlay.tags" :key="item.id">
                {{item.name}}
            </text>
        </view>
    </view>
</template>

<script>
export default {
    data(){
        return {
            videoPlay: ""
        }
    },
    onLoad(){
        let that = this;
        uni.getStorage({
            key: "videoItem_key",
            success(res){
                let data = res.data.data.content.data;
                that.videoPlay = data;
            }
        })
    },
    methods:{
        getHeight(){
            let text = uni.createSelectorQuery().select(".video-description");
            text.fields({
                
                context: true
            },data=>{
                console.log(data);
            }).exec()
            
        }
    }
}
</script>

<style>
    .video-play video{
        width: 100%;
    }

    .video-author{
        width: 100%;
        margin: 4px 0;
        display: flex;
        flex-direction: row;
        align-items: center;
        border-bottom: 1px solid #ccc;
        box-shadow: 0 5px 7px rgb(233, 233, 233);
        padding-bottom: 5px;
    }
    .video-author image{
        width: 75upx;
        height: 75upx;
        border-radius: 50%;
        margin: 0 10px 0 20px;
    }
    .video-author text{
        font-size: 30upx;
        flex: 1;
    }
    .video-author view{
        font-size: 26upx;
        padding: 5px 8px;
        background: #ccc;
        border-radius: 5px;
        margin: 0 20px 0 10px;
    }

    .video-content{
        margin: 20px 20px 2px;
        padding-bottom: 20upx;
        border-bottom: 1px solid #ccc;
    }
    .video-content .video-description{
        font-size: 34upx;
    }
    .video-content .video-description-art{
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
        word-wrap: break-word;
        white-space: normal;
        -webkit-line-clamp: 1;
        -webkit-box-orient: vertical; 
    }
    .video-content .video-consumption{
        color: rgb(161, 161, 161);
        font-size: 28upx;
        margin: 15upx 0 5upx;
    }
    .video-content .video-consumption text{
        padding: 3upx 24upx 3px 0;
    }
    .video-content .video-title{
        color: rgb(161, 161, 161);
        font-size: 28upx;
    }

    .video-tags{
        margin: 0 20px;
    }
    .video-tags text{
        font-size: 28upx;
        padding: 4upx 10upx;
        margin: 3px 0;
        background: #ddd;
        border-radius: 5px;
        margin-right: 15upx;
        word-wrap:break-word; 
        word-break:break-all; 
        display: inline-block;
        color: #fff;
    }
</style>
