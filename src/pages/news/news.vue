<template>
    <view>
        <view class="title-view">
            <text class="title-text">
                {{title}}
            </text>
        </view>
        
        <view class="news-list">
            <view class="news-item" v-for="(item,index) in newsList" :key="index">
                <view class="news-pic">
                    <image :src="item.picUrl"></image>
                </view>
                <view class="news-content">
                    <text class="news-title">
                        {{item.title}}
                    </text>
                    <view class="news-desc">
                        <text>
                            {{item.description}}
                        </text>
                        <text>
                            {{item.ctime}}
                        </text>
                    </view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
import tianxing from '../../tianxing'
import { setTimeout } from 'timers';
export default {
    data(){
        return{
            title: "",
            nameid: '',
            newsList: "",
            num: 10
        }
    },
    onLoad(option){
        let that = this;
        that.title = option.name;
        that.nameid = option.id;
        uni.request({
            url: tianxing.TXAPI_BASE_URL +"/"+ option.id +"/",
            data: {
                key: tianxing.TXAPI_KEY,
                num: that.num
            },
            success(res){
                that.newsList = res.data.newslist;
            }
        })
    },
    onReachBottom(){
        let that = this;
        uni.showLoading({title:'玩命加载中'});
        that.num += 10;
        if (that.num < 50){
            uni.request({
                url: tianxing.TXAPI_BASE_URL +'/'+ that.nameid +'/',
                data: {
                    key: tianxing.TXAPI_KEY,
                    num: that.num
                },
                success(res){
                    that.newsList = res.data.newslist;
                    uni.hideLoading();
                }
            })
        } else {
            uni.showToast({title:'已经到底了'});
            setTimeout(function(){
                uni.hideToast();
            },1500)
        }
    }
}
</script>

<style>
    .title-view{
        margin: 20px;
    }
    .title-text{
        padding: 20upx 35upx;
        font-size: 75upx;
        font-weight: 700; 
        border-bottom: 5px solid #ccc;
        background: linear-gradient(25deg,#000,#bbb);
        -webkit-text-fill-color: transparent;
        background-clip: text;
    }

    .news-list{
        margin: 0 20px;
        display: block;
    }
    .news-item{
        margin: 15upx 0 25upx;
        box-sizing: border-box;
        border: 2px solid #ccc;
        border-left: 1px;
        border-right: 1px;
        padding-bottom: 4upx;
        border-radius: 20px;
        overflow: hidden;
    }
    .news-pic{
        width: 100%;
    }
    .news-pic image{
        width: 100%;
    }
    .news-title{
        padding: 10upx;
    }
    .news-desc{
        padding: 0 10upx;
        font-size: 34upx;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        color: #ccc;
        margin-bottom: 10px;
    }
</style>
