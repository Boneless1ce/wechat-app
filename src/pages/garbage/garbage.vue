<template>
    <view class="container">
        <func-title>
            请问你是什么垃圾？
        </func-title>

        <view class="func-content">
            <view class="func-input">
                <input type="text" placeholder="垃圾分类，保护环境，从你我做起" @input="getData" :value="inputValue">
            </view>
            
            <scroll-view class="func-list" v-show="sourceList">
                <view :id="index" class="func-item" v-for="(item,index) in sourceList" :key="item.id" @click="getShow">
                    {{ item.name }}
                </view>
            </scroll-view>
        </view>

        <view class="func-show" v-if="showItem">
            <text>
                名称 : {{ showItem.name }}
            </text>
            <view class="func-type">
                <text v-if="showItem.type == 0">
                    可回收垃圾
                </text>
                <text v-else-if="showItem.type == 1">
                    有害垃圾
                </text>
                <text v-else-if="showItem.type == 2">
                    厨余（湿）垃圾
                </text>
                <text v-else-if="showItem.type == 3">
                    其他（干）垃圾
                </text>
            </view>
            <text>
                解释：{{showItem.explain}}
            </text>
            <text>
                包含物品：{{showItem.contain}}
            </text>
            <text>
                投放提示：{{showItem.tip}}
            </text>
        </view>

        <view class="func-show" v-if="!showItem">
            <image src="../../static/09d77a8bb15b9fe81f28dd3b8aa7d78.jpg"></image>
        </view>
    </view>
</template>

<script>
import funcTitle from '../../components/funcTitle'
import tianxing from '../../tianxing'
export default {
    data() {
        return {
            inputValue: '',
            sourceList: '',
            showItem: ''
        }
    },
    methods: {
        getData(e){
            let value = e.detail.value;
            let that = this;
            if(value != ''){
                uni.request({
                    url: tianxing.TXAPI_BASE_URL +'/txapi/lajifenlei/',
                    data: {
                        key: tianxing.TXAPI_KEY,
                        word: value,
                    },
                    success(res){
                        if(res.data.code == 200){
                            that.sourceList = res.data.newslist;
                        }
                    }
                })
            }
        },
        clean(e){
            this.sourceList = '';
            let value = e.detail.value;
            let that =this;
            if(value != ''){
                uni.request({
                    url: tianxing.TXAPI_BASE_URL +'/txapi/lajifenlei/',
                    data: {
                        key: tianxing.TXAPI_KEY,
                        word: value,
                    },
                    success(res){
                        if(res.data.code == 200){
                            that.showItem = res.data.newslist[0]
                        }
                    }
                })
            }
        },
        getShow(e){
            this.showItem = this.sourceList[e.target.id];
            this.inputValue = this.showItem.name;
            this.sourceList = '';
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
        z-index: 99;
    }
    .func-input input{
        height: 80upx;
        padding: 10upx 30upx;
        background: #f6f6f6;
    }

    .func-content{
        position: relative;
    }
    .func-list{
        position: absolute;
        top: 86upx;
        left: 0;
        background: #fffefe;
        box-sizing: border-box;
        border: 1px solid #000;
        border-top: none;
        border-bottom-left-radius: 20upx;
        border-bottom-right-radius: 20upx;
    }
    .func-list .func-item{
        padding: 10upx 30upx;
    }
    .func-list .func-item:first-child{
        margin-top: 16upx
    }

    .func-show{
        margin-top: 30px;
        width: 100%;
    }
    .func-show text{
        margin: 15upx 0;
    }
    .func-show image{
        display: block;
        width: 100%;
        border-radius: 20upx;
        overflow: hidden;
    }
    .func-type{
        font-weight: 700;
    }
</style>
