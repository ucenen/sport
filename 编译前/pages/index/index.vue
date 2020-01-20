<template>
	<view class="content">
		<view class="time_box">
			<view class="time">
				2020年1月24日 — 1月30日
			</view>
			<image src="../../static/1.png" class="time_img" @tap="showMask(1)"></image>
		</view>
		<!-- 基础信息 -->
		<view class="user">
			<view class="user_list" style="width: 35%;">
				<view class="user_title">
					姓名:
				</view>
				<view class="user_con">
					李丽丽
				</view>
			</view>
			<view class="user_list" >
				<view class="user_title" >
					手机:
				</view>
				<view class="user_con">
					17777778888
				</view>
				<view class="user_btn">
					修改
				</view>
			</view>
		</view>
		<view class="user" style="padding-top: 0px;">
			
			<view class="user_list" >
				<view class="user_title" >
					我的邀请码:
				</view>
				<view class="user_con">
					{{code}}
				</view>
				<view class="user_btn" @tap="copy">
					复制
				</view>
			</view>
		</view>
		<view class="user" style="padding-top: 0px;">
			
			<image src="../../static/3.png" mode="" style="width: 50vw;height: 10vw;"  @tap="showMask(4)"></image>
		</view>
		<view style="height: 50rpx;"></view>
		
		<!-- 游戏 -->
		<!-- <view class="game_box">
			<view class="game_con">
				
			</view>
		</view> -->
		
		
		<gracePage headerBG="#D8043E" :customHeader="false">
				<view slot="gBody" style="display: flex;justify-content: center;">
					<view class="lottery-draw-main-bg">
						<view class='lottery-draw-main'>
							<block v-for="(item, index) in prizes" :key="index">
								<view :class="['lottery-draw-main-items', animateIndex == index ? 'lottery-draw-animate' : '']" v-if="index != 4&&index != 3" >
									<image :src="item.imgurl" class="lottery-draw-main-img" mode='widthFix'></image>
									
								</view>
								<view :class="['lottery-draw-main-items', animateIndex == index ? 'lottery-draw-animate' : '']" v-if="index == 3">
									<image :src="item.imgurl" class="lottery-draw-main-img" mode='widthFix'></image>
									
								</view>
								<view :class="['lottery-draw-main-items','lottery-draw-main-btn', animateStatus == 'ing' ? 'breath_light' : '']" v-if="index == 4" @tap='go'>
									<image :src="item.imgurl" class="lottery-draw-main-img" mode='widthFix'></image>
								</view>
							</block>
						</view>
					</view>
					
				</view>
			</gracePage>
			
			<!-- 下载 -->
			
			<view style="width: 100%;font-size: 42rpx;color: #fff;text-align: center;letter-spacing: 3rpx;padding: 88rpx 0 110rpx 0;font-weight: bold;">全民体育 APP任务</view>
			
			
			<!-- 列表 -->
			<view class="list_box">
				<view class="list" v-for="(item,index) in list" :key="index">
					<image class="list_left_img" :src="item.img" mode="widthFix"></image>
					<view class="list_mind">
						<view class="list_mind_top">
							{{item.title}} <view v-if="item.id==1 || item.id==2" class="list_top_r">{{item.bg}}</view>
						</view>
						<view class="des">
							{{item.des}}
						</view>
					</view>
					<view class="list_right"  @tap="showMask(3)">
						<image v-if="item.id!=3" src="../../static/17.png" mode="widthFix"></image>
						<image v-else src="../../static/15.png" mode="widthFix"></image>
					</view>
				</view>
				<view class="list_btomm">
					<a href="https://171tiyu.com/app"><image src="../../static/20.png" mode="widthFix" class="down_img"> </image></a>
					<view class="record" @tap="showMask(2)" >
						获奖记录
					</view>
				</view>
			</view>
			<view style="height: 100rpx;"></view>
			
			<!-- 弹框 -->
			<view class="mask" v-if="status" @tap.stop="colseMask">
				
				<view class="mask_box">
					<!-- 活动规则 -->
					<view class="mask_role" v-if="status_role">
						<view class="mask_role_title">
							活动规则
						</view>
						<view class="mask_role_ul">
							<view class="mask_role_list" v-for="(item,index) in role" :key="index">
								{{item}}
							</view>
						</view>
					</view>
					<!-- 获奖记录 -->
					<view class="mask_role" v-if="status_reward" @tap='jl' >
						<view class="mask_role_title">
							获奖记录
						</view>
						<view class="mask_role_ul">
							<view class="mask_reward">
									<view class="mask_reward_time">
										时间
									</view>
									<view class="mask_reward_thing">
										奖励
									</view>
							</view>
							<view class="mask_reward" v-for="(item,index) in reward" :key="index">
									<view class="mask_reward_time" style="font-size: 27rpx;font-weight: 600;color: #666;">
										{{item.time}}
									</view>
									<view class="mask_reward_thing" style="font-size: 27rpx;font-weight: 600;color: #666;">
										{{item.reward}}
									</view>
							</view>
						</view>
					</view>
					
					<!-- 填写信息 -->
					<view class="mask_user" v-if="status_user" @tap.stop="showMask(3)">
						
						<view class="mask_user_list">
							<view class="mask_user_title">
								姓名
							</view>
							<input type="text" value="" class="mask_user_input" placeholder="请输入姓名" />
						</view>
						<view class="mask_user_list">
							<view class="mask_user_title">
								手机号码
							</view>
							<input type="text" value="" class="mask_user_input" placeholder="请输入手机号码" />
						</view>
						<view class="mask_btn_con" @tap="qdlq">
							<view class="mask_btn">
								确定
							</view>
						</view>
					</view>
					
					<!-- 填写邀请码 -->
					<view class="mask_user" v-if="status_code" @tap.stop="showMask(4)">
						
						<view class="mask_user_list">
							<view class="mask_user_title" >
								邀请码
							</view>
							<input type="text" value="" class="mask_user_input" placeholder="请输入邀请码" />
						</view>
						
						<view class="mask_btn_con"@tap="yqm" >
							<view class="mask_btn">
								确定
							</view>
						</view>
					</view>
				</view> 
				
				
				
				
				
			</view>
	</view>
</template>

<script>
	
	import clipboard from "@/common/dc-clipboard/clipboard.js"
	import gracePage from "../../components/gracePage.vue";
	import graceSpeaker from "../../components/graceSpeaker.vue";
	var animateTimer = null;
	export default {
	    data() {
	    	return {
				status:false,
				status_role:false,
				status_reward:false,
				status_user:false,
				status_code:false,
				code:'17777778888',
				speakerMsgs: [
					{ title: "用户 *** 刚刚抽中一台 iphoneX", url: "", opentype: "navigate" },
					{ title: "用户 *** 刚刚抽中跑鞋", url: "", opentype: "navigate" }
				],
				// 奖品及按钮
				prizes : [
				  { title: '5元红包', 'imgurl': "../../static/40.png" },
				  { title: '1元红包', 'imgurl': "../../static/41.png" },
				  { title: '0.2元红包', 'imgurl': "../../static/42.png" },
				  { title: '腾讯视频会员', 'imgurl': "../../static/47.png" },
				  { title: 'GO', 'imgurl': "../../static/28.png" },
				  { title: '球鞋', 'imgurl': "../../static/46.png" },
				  { title: '0.1元红包', 'imgurl': "../../static/43.png" },
				  { title: '2元红包', 'imgurl': "../../static/44.png" },
				  { title: '10元红包', 'imgurl': "../../static/45.png" },
				],
				// 转圈 index
				turnIndex : 0,
				// 动画 index
				animateIndex : -1,
				// 动画 执行状态 stop 停止 ing 执行中 end 结束
				animateStatus : 'stop' ,
				list:[
					{
						id:1,
						img:'../../static/34.png',
						title:'邀请拉新奖励',
						bg:'(1/3)',
						des:'新人输入邀请码，老用户即可获得奖励',
					},
					{
						id:2,
						img:'../../static/34.png',
						title:'APP新人奖励',
						bg:'新人专属',
						des:'1月24日后注册的新用户可领取（仅限一次）',
					},
					{
						id:3,
						img:'../../static/35.png',
						title:'每日登录奖励',
						bg:'',
						des:'每日登录APP，抽奖次数 +1',
					},
					{
						id:4,
						img:'../../static/36.png',
						title:'每日分享奖励',
						bg:'',
						des:'分享本次活动，即可领取奖励',
					}
				],
				role:[
					'1. 活动期间，用户每天可以获得1次抽奖机会。',
					'2. 完成APP专属任务，可以获得额外奖励',
					'3. 活动奖励会在2月3日后由客服 【NationalSports】统一发放',
					'4. 请获奖用户添加客服微信，领取相应的奖励',
				],
				
				reward:[
					{
						id:1,
						time:'12月30日',
						reward:"1元红包*1"
					},
					{
						id:2,
						time:'12月30日',
						reward:"拉新红包5元*1"
					},
					{
						id:3,
						time:'12月30日',
						reward:"分享红包0.5元*1"
					},
					{
						id:4,
						time:'12月30日',
						reward:"视频VIP*1"
					}
				]
			}
	    },
		methods:{
			// 关闭mask
			colseMask(){
				this.status=false;
				this.status_role=false;
				this.status_reward=false;
				this.status_user=false;
				this.status_code=false;
				
			},
			//输入邀请码
			// yqm(){
			// uni.request({
			// 				    url: 'http://18.182.218.232:8081/v2/event/2020-newYear-inviteCode/user/inviteCode', 
			// 				    data: {
							        
			// 				    },
			// 					dataType:"jsonp",
			// 				    header: {
			// 						 'uid':'116186',
			// 			            'token':'KvwAJ72Pl7crsmLAMO//+bcE1AvFl5TRTCucHaxVzeycZTz7I9quD39QaTL83hx1/TEszE/dJjToXYHo/aii3UBGH6gR7v48oCO7g1ELuLI2Vrih5nuzxFex0AgfguyQhPbyNglo2ruS2XofYf74wNrjrt62wBMoeLE8Wk12n8c='
			// 				    },
			// 				    success: (res) => {
			// 				        console.log(res);
							       
			// 				    }
			// 				});
			// 				}, 
			
			// 复制邀请码
			copy(){
				uni.setClipboardData({ data:this.code, success:function(data){uni.showToast({title:'复制成功', icon:"none"});}, fail:function(err){}, complete:function(res){} })
			
			// qdlq(){
			// 	uni.request({
			// 	     url:'http://18.182.218.232:8081/v2/event/2020-newYear-register/user/award',
			// 	     data:{
			// 	      text:'uni.request'
			// 	     },
			// 	     headers:{
			// 	      'uid':'116186',
			// 	      'token':'KvwAJ72Pl7crsmLAMO//+bcE1AvFl5TRTCucHaxVzeycZTz7I9quD39QaTL83hx1/TEszE/dJjToXYHo/aii3UBGH6gR7v48oCO7g1ELuLI2Vrih5nuzxFex0AgfguyQhPbyNglo2ruS2XofYf74wNrjrt62wBMoeLE8Wk12n8c='
			// 	     },
			// 	     success:res =>{
				     
			// 	     console.log(res.data);
			// 	     this.text = 'request success'
			// 	     }
				     
			// 	    })
			// 	   }
				    
			// 	   },
				
				
			// }
			
			// yqm(){
			//     uni.request({
			//      url:'http://18.182.218.232:8081/v2/event/2020-newYear-inviteCode/user/awardStatus',
			//      data:{
			//       text:'uni.request'
			//      },
			//      headers:{
			//       'uid':'116186',
			//       'token':'KvwAJ72Pl7crsmLAMO//+bcE1AvFl5TRTCucHaxVzeycZTz7I9quD39QaTL83hx1/TEszE/dJjToXYHo/aii3UBGH6gR7v48oCO7g1ELuLI2Vrih5nuzxFex0AgfguyQhPbyNglo2ruS2XofYf74wNrjrt62wBMoeLE8Wk12n8c='
			//      },
			//      success:res =>{
			     
			//      console.log(res.data);
			//      this.text = 'request success'
			//      }
			     
			//     })
			//    }
			    
			//    },
				
			},
			//显示
			showMask(e){
				if(e==1){
					this.status=true;
					this.status_role=true;
					this.status_reward=false;
					this.status_user=false;
					this.status_code=false;
				}
				if(e==2){
					this.status=true;
					this.status_role=false;
					this.status_reward=true;
					this.status_user=false;
					this.status_code=false;
				}
				if(e==3){
					this.status=true;
					this.status_role=false;
					this.status_reward=false;
					this.status_user=true;
					this.status_code=false;
				}
				if(e==4){
					this.status=true;
					this.status_role=false;
					this.status_reward=false;
					this.status_user=false;
					this.status_code=true;
					
				}
			},
			// 抽奖动画
			go : function(){
				// 用户如果已经抽过奖或者不满足条件这里使用 return 返回，终止程序运行
				// your code ...
	             
				// 判断是否正在执行动画
				if (this.animateStatus != 'stop'){return false;}
				this.animateStatus = 'ing';
	
				// 此处根据自己的业务决定抽奖结果[ 算法可以是后端或前端 自行百度根据自己概率做算法 ]
	             
				// 比如模拟一个随机 0 - 8 数字[ 中奖率极高 ]
				var num = Math.floor(Math.random() * 8);
				// 不能抽中按钮所以抽中按钮等没中奖
				if(num == 4){num = 8;}
				// num 代表奖品的 index 应该使用自己的算法得出
				 
				// 动画
				this.animate(num);
			  },
			  animate:function(num){
				//执行动画 100 代表动画切换时间可以调整动画速度
				this.turnIndex    = 0;
				this.animateIndex = 0;
				animateTimer = setInterval(() => {this.turn(num);}, 100);
			  },
			  turn : function(num){
				var orders = [0, 1, 2, 5, 8, 7, 6, 3]; //奖品序号
				var turnNumForPrizes = 0; //奖品的位置
				for(var i = 0; i < orders.length; i++){
				  if (orders[i] == num){
					turnNumForPrizes = i;
					break;
				  }
				}
				var turnNum = 3; //此处设置预先转几圈
				if (this.turnIndex >= 8 * turnNum + turnNumForPrizes){
				  clearInterval(animateTimer) ; 
				  // 动画结束 此处可以进行后续操作
				  this.animateStatus = 'stop'; // 可以继续抽奖
				  // this.animateStatus = 'end'; // 这样写就可以结束抽奖
	
				  if(num == 8){
					uni.showToast({
					  title: '感谢参与 ^_^',
					  icon:"none"
					});
				  }else{
					uni.showToast({
					  title: '恭喜您！抽中了 : ' + this.prizes[num].title,
					  icon: "none"
					});
				  }
				  // your code ...
				  const requestTask = uni.request({
				            url: 'http://18.182.218.232:8081/v2/event/2020-newYear-lottery/lottery/info', 
				           
				         data: {
				             },
				           headers: {
				                  'uid': '116186' ,
				            'token':'KvwAJ72Pl7crsmLAMO//+bcE1AvFl5TRTCucHaxVzeycZTz7I9quD39QaTL83hx1/TEszE/dJjToXYHo/aii3UBGH6gR7v48oCO7g1ELuLI2Vrih5nuzxFex0AgfguyQhPbyNglo2ruS2XofYf74wNrjrt62wBMoeLE8Wk12n8c='
				             },
				            success: function(res) {
				                console.log(res.data);
				            }
				        });
				  //
				  return ;
				}
				this.turnIndex++;
				var animateIndex  = this.turnIndex % 8;
				this.animateIndex = orders[animateIndex];
			}
		},
		components:{gracePage, graceSpeaker}
	}
</script>





<style>
	.content {
		width: 100%;
		min-height: 100vh;
		background: url(../../static/bg.png);
		background-size: 100% 165%;
	}
	.time_box{
		padding-top: 550rpx;
		display: flex;
		flex-wrap: nowrap;
		align-items: center;
		justify-content: center;
	}
	.time{
		font-size: 40rpx;
		color: #fff;
		font-weight: bold;
	}
	.time_img{
		width: 50rpx;
		height: 50rpx;
		display: block;
		position: relative;
		top: -30rpx;
	}
	.user{
		width: 100%;
		box-sizing: border-box;
		padding: 40rpx 30rpx;
		display: flex;
		justify-content: center;
		flex-wrap: nowrap;
	}
	.user_list{
		display: flex;
		flex-wrap:nowrap;
		align-items: center;
		font-size: 28rpx;
		color: #fff;
		font-weight: bold;
	}
	.user_title{
		
		text-align: center;
	}
	.user_con{
		
		text-align: left;
		padding: 0 25rpx;
	}
	.user_btn{
		width: 100rpx;
		height: 50rpx;
		line-height: 50rpx;
		background: url(../../static/2.png);
		background-size: 100% 100%;
		text-align: center;
		font-size: 23rpx;
	}
	.game_box{
		box-sizing: border-box;
		width: 90%;
		margin: 0 auto;
		background: url(../../static/27.png);
		background-size: 100% 100%;
		padding: 6vw;
	}
	.game_con{
		width: 100%;
		box-sizing: border-box;
		background: #fff;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		height: 78vw;
	}
	
	.lottery-draw-banner{width:100%;}
	.lottery-draw-msg{width:550rpx; border:2rpx solid #FC5566; border-radius:50px; color:#E81B54; background-color:rgba(255, 255,255, 0.8); padding:0rpx 30rpx; margin-left:70rpx;}
	.lottery-draw-main-bg{width:600rpx; height:540rpx; padding:30rpx; border-radius:10px; margin:30rpx 60rpx; background: url(../../static/27.png);background-size: 100% 100%;}
	.lottery-draw-main{width:570rpx; height:510rpx; padding:12rpx;border-radius:8px; display:flex; flex-wrap:wrap; justify-content:space-between;}
	.lottery-draw-main-items{width:188rpx; height:168rpx;background-size: 100% 100%; margin:3rpx 0; overflow:hidden;border-radius: 30rpx;display: flex;flex-direction: column;justify-content: center;}
	.lottery-draw-main-btn{background-color:#FFB001; border-color:#FFB001; color:#AB6120; text-align:center; line-height:163rpx; font-weight:700; font-size:50rpx;}
	.lottery-draw-main-img{width:188rpx; height:168rpx !important; margin:0 auto; overflow:hidden;}
	.lottery-draw-main-name{line-height:40rpx; height:40rpx; overflow:hidden; text-align:center; color:#AB6120; font-size:22rpx;}
	.lottery-draw-animate{border:4rpx solid #FFD800 !important;box-sizing: border-box;}
	@keyframes breath { from { opacity: 1; }   75%  { opacity: 0.9; }  50%  { opacity: 0.8; }  25%  { opacity: 0.9; }  to   { opacity: 1; }   }
	.breath_light{animation:breath 1s infinite linear;}
	.download{
		width: 100%;
		padding: 100rpx 0;
		display: flex;
		justify-content: center;
	}
	.download image{
		width: 60vw;
		height: 90rpx !important;
		overflow: visible;
	}
	.list_box{
		width: 660rpx;
		box-sizing: border-box;
		padding: 20rpx 30rpx 5rpx 20rpx;
		background: #FF484C;
		border-radius: 10rpx;
		margin: 0 auto;
	}
	.list{
		width: 100%;
		background: #fff;
		border-radius: 5rpx;
		margin-bottom: 20rpx;
		display: flex;
		flex-wrap: nowrap;
		align-content: center;
	}
	.list_mind_top{
		width: 100%;
		display: flex;
		align-items: center;
		padding-bottom: 7rpx;
		font-size: 28rpx;
		color: #333;
		font-weight: bold;
	}
	.list_top_r{
		margin-left: 20rpx;
		height: 30rpx;
		line-height: 30rpx;
		background: url(../../static/16.png);
		background-size: 100% 100%;
		width: 110rpx;
		text-align: center;
		color: #fff;
		font-size: 20rpx;
	}
	.des{
		width: 80%;
		font-size: 22rpx;
		color: #666;
		line-height: 30rpx;
	}
	.list_left_img{
		width: 21vw !important;
		height: 18vw !important;
		display: block;
	}
	.list_mind{
		flex: 1;
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		justify-content: center;
		padding-left: 10rpx;
	}
	.list_right{
		width: 18vw;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	.list_right image{
		width: 14vw !important;
		height: 50rpx !important;
		display: block;
		margin: 0 auto;
	}
	.list_btomm{
		width: 100%;
		height: 150rpx;
		line-height: 150rpx;
		display: flex;
		flex-direction: column;
		justify-content: center;
		position: relative;
	}
	.down_img{
		width: 45vw;
		height: 7vw !important;
		display: block;	
		margin: 0 auto;
	}
	.record{
		height:40rpx;
		line-height: 40rpx;
		display: inline-block;
		font-size: 27rpx;
		color: #fff;
		border-bottom: 1px solid #fff;
		color: #fff;
		position: absolute;
		left: 0;
		top: 55rpx;
	}
	.mask{
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		background: rgba(0,0,0,0.7);
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	.mask_box{
		width: 85%;
		box-sizing: border-box;
		padding: 20rpx;
		background: #FF484C;
		border-radius: 10rpx;
		margin: 0 auto;
	}
	.mask_role{
		width: 100%;
	}
	.mask_role_title{
		padding: 30rpx 0;
		padding-top: 0;
		text-align: center;
		font-size: 45rpx;
		color: #fff;
		font-weight: bold;
		letter-spacing: 10rpx;
	}
	.mask_role_ul{
		width: 100%;
		box-sizing: border-box;
		padding:30rpx 30rpx;
		background: #fff;
		border-radius: 10rpx;
	}
	.mask_role_list{
		width: 100%;
		padding: 10rpx 0;
		font-size: 28rpx;
		color: #333;
		line-height: 40rpx;
	}
	.mask_reward{
		width: 100%;
		display: flex;
		flex-wrap: nowrap;
		align-items: center;
		padding: 20rpx 0;
	}
	.mask_reward_time{
		width: 40%;
		font-size: 33rpx;
		color: #333;
		font-weight: bold;
		text-align: center;
	}
	.mask_reward_thing{
		width: 60%;
		font-size: 33rpx;
		color: #333;
		font-weight: bold;
		text-align: center;
	}
	.mask_user{
		width: 100%;
		box-sizing: border-box;
		padding: 70rpx 20rpx;
		background: #FFF6BD;
		border-radius: 10rpx;
		margin: 0 auto;
	}
	.mask_user_list{
		width: 100%;
		margin: 30rpx 0;
		display: flex;
		align-items: center;
		flex-wrap: nowrap;
		background: #fff;
		border-radius: 10rpx;
		height: 80rpx;
		line-height: 80rpx;
		box-sizing: border-box;
		padding: 0 25rpx;
	}
	.mask_user_title{
		color: #555;
		font-size: 28rpx;
		letter-spacing: 5rpx;
	}
	.mask_user_input{
		flex: 1;
		padding-left:15rpx;
		color: #555;
		font-size: 28rpx;
	}
	.mask_btn_con{
		width: 100%;
		display: flex;
		justify-content: center;
		padding: 80rpx 0 0rpx 0;
	}
	.mask_btn{
		width: 170rpx;
		height: 60rpx;
		line-height: 60rpx;
		text-align: center;
		color: #fff;
		font-size: 28rpx;
		border-radius: 10rpx;
		background: #FDC401;
		letter-spacing: 20rpx;
	}
</style>
