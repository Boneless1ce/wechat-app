<template>
    <view class="container">
        <func-title>
            未来七天天气查询
        </func-title>

        <view class="func-input">
            <input type="text" v-model="city">
            <button @click="getWeather">查询</button>
        </view>

        <view class="func-hint">
            <view class="func-hint-item" v-for="(item,index) in weatherList" :key="index">
                
                    <view class="item-left">
                        <view class="item-date">
                            {{item.date}}
                        </view>
                        <view class="item-week">
                            {{item.week}}
                        </view>
                        <view class="item-weather">
                            {{item.weather}}
                        </view>
                    </view>

                    <view class="item-right">
                        <view class="item-temp font-bg">
                            <text>
                                {{item.lowest}}
                            </text>
                            <text>
                                ~
                            </text>
                            <text>
                                {{item.highest}}
                            </text>
                        </view>
                        <view class="item-winds font-sm">
                            <view class="item-wind">
                                <text>风向 :</text>
                                {{item.wind}}
                            </view>
                            <view class="item-windspeed">
                                <text>风速 :</text>
                                {{item.windspeed}}
                            </view>
                        </view>
                    </view>
                
            </view>
        </view>
    </view>
</template>

<script>
import funcTitle from '../../components/funcTitle'
import tianxing from '../../tianxing'
export default {
    data(){
        return {
            city: '广州',
            weatherList: ''
        }
    },
    onLoad(){
        let that = this;
        uni.request({
            url: tianxing.TXAPI_BASE_URL +'/txapi/tianqi/',
            data: {
                key: tianxing.TXAPI_KEY,
                city: that.city,
            },
            success(res){
                that.weatherList = res.data.newslist;
            }
        })
    },
    methods: {
        getWeather(){
            let that = this;
            if(this.city != ''){
                uni.showToast({title:"Loading"})
                uni.request({
                    url: tianxing.TXAPI_BASE_URL +'/txapi/tianqi/',
                    data: {
                        key: tianxing.TXAPI_KEY,
                        city: that.city,
                    },
                    success(res){
                        uni.hideToast();
                        if(res.data.code == 200) {
                            that.weatherList = res.data.newslist;
                        } else {
                            uni.showModal({
                                title: "提示",
                                content: res.data.msg
                            })
                        }
                    }
                })
            } else {
                uni.showModal({
                    title: "提示",
                    content: '请输入城市'
                })
            }
        }
    },
    components: {
        funcTitle
    }
}
</script>

<style scoped>
    .container{
        margin: 0 20px;
    }

    .func-input{
        border: 1upx solid #000;
        border-radius: 20upx;
        overflow: hidden;
        display: flex;
        flex-direction: row;
    }
    .func-input input{
        height: 80upx;
        padding: 10upx 30upx;
        background: #f6f6f6;
        flex: 1;
    }
    .func-input button{
        outline: none;
        border: none;
        margin: 0;
    }

    .func-hint-item{
        width: 100%;
        border-radius: 20upx;
        background: rgb(70, 157, 255);
        color: #fff;
        margin: 30upx 0;
        text-align: center;
        display: flex;
        flex-direction: row;
    }
    .item-left{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding: 10upx 20upx;
    }
    .item-right{
        flex: 1;
        display: flex;
        flex-direction: column;
        padding: 10upx 20upx;
        justify-content: space-between;
    }
    .item-temp{
        padding-top: 20upx;
    }
    .item-winds{
        display: flex;
        flex-direction: row;
        justify-content: space-around;
    }
    .font-bg{
        font-size: 1.5em;
    }
    .font-sm{
        font-size: 0.7em;
    }
</style>
