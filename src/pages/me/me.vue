<template>
    <div class="container">
        <div class="user-info">
            <div class="info-touxiang">
                <open-data type="userAvatarUrl"></open-data>
            </div>
            <div class="info-content">
				<div class="info-name">
					<open-data type="userNickName"></open-data>
				</div>
				<div class="info-address">
					<open-data type="userCountry" lang="zh_CN"></open-data>
					<open-data type="userProvince" lang="zh_CN"></open-data>
				</div>
                
            </div>
        </div>
        
		<div class="list">
			<div class="list-item" v-for="item in mineList" :key="item.route" @click="goRouter(item)">
				<div class="list-icon">
					<img :src="item.icon">
				</div>
				<div class="list-text">
					{{item.name}}
				</div>
			</div>
		</div>
		
		<div class="list">
			<div class="list-item" v-for="item in funcList" :key="item.route" @click="goRouter(item)">
				<div class="list-icon">
					<img :src="item.icon">
				</div>
				<div class="list-text">
					{{item.name}}
				</div>
			</div>
		</div>
    </div>
</template>

<script>
export default{
	data() {
		return {
			mineList:[{
				name: "我的收藏",
				route: "collection",
				icon: "../../static/collection.png"
			},{
				name: "稍后观看",
				route: "watch",
				icon: "../../static/watch-later.png"
			}],
			funcList:[{
				name: "垃圾分类",
				route: "garbage",
				icon: "../../static/laji.png"
			},{
				name: "天气预报",
				route: "weather",
				icon: "../../static/tianqi.png"
			},{
				name: "老黄历",
				route: "calendar",
				icon: "../../static/rili.png"
			}]
		}
	},
	methods: {
		goRouter(item){
			uni.navigateTo({
				url: `../../pages/${item.route}/${item.route}`
			});
		}
	}
}
</script>

<style scoped>
    .container{
        background-color: #fff
    }
    .user-info{
        background-color: #f2f2f2;
		padding: 34upx;
        display: flex;
		flex-direction: row;
		align-items: center;
		flex: 0;
		border-bottom-left-radius: 20upx;
		border-bottom-right-radius: 20upx;
    }
    .user-info .info-touxiang{
        width: 140upx;
        height: 140upx;
		border-radius: 14upx;
		overflow: hidden;
    }
	.user-info .info-content{
		height: 160upx;
		padding-left: 10px;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
	}
	.user-info .info-content .info-address{
		font-size: 28upx;
	}
	
	.list{
		margin-top: 60upx;
		padding: 20upx 0;
		background: #F2F2F2;
		border-radius: 20upx;
	}
	.list-item{
		padding: 15upx 0;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.list-item .list-icon img{
		display: block;
		padding: 0 20upx;
		width: 56upx;
		height: 56upx;
	}
	.list-item .list-text{
		font-size: 32upx;
	}
</style>

