<template>
	<view @touchstart="touchStart" @touchend="touchEnd" @touchmove="touchMove">
	<!-- <view v-for="(words, index) in list" :key="words.id">
		<text>{{words.word}}--{{words.translation}}</text>
	</view> -->
	<view>
		<text>score:{{score}}</text>
		<button @click="clickBtm()" class="Btm">随机选择题目</button>
		<text class="textForm">{{randomQue}}</text>
		<input type="text" v-model="userAnswer" @confirm="checkAnswer" class="inputCon" />
		<text>{{giveBack}}</text>
		<button @click="clickBtm2()" class="Btm">随机选择释义</button>
		<text class="textForm">{{randomTrans}}</text>
		<input type="text" v-model="userAnswer2" @confirm="checkAnswer2" class="inputCon"/>
		<text>{{giveBack2}}</text>
		<button type="text" @click="ChooseWord()">跳转</button>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				lists:[],
				randomQue:'',
				userAnswer:'',
				giveBack:'',
				score:0,
				randomTrans:'',
				userAnswer2:'',
				giveBack2:'',
				startX:'',
				endx:'',
				threshold:''
			};
		},
		onLoad() {
			this.lists=require("@/static/nihon.json");
			
		},
		
		methods: {
			clickBtm(){
				const randomIndex = Math.floor(Math.random()*this.lists.length);
				this.randomQue = this.lists[randomIndex].word;
				this.randomAns = this.lists[randomIndex].translation;
					
				if(this.userAnswer){
					this.userAnswer='';
				}
				if(this.giveBack){
					this.giveBack='';
				}
			},
				
			checkAnswer(){
				if(this.userAnswer===this.randomAns){
					//this.giveBack='right!';
					this.clickBtm();
					this.score++;
				}else{
					this.giveBack='no'
				}
			},
			clickBtm2(){
				const randomIndex2 = Math.floor(Math.random()*this.lists.length);
				this.randomTrans = this.lists[randomIndex2].translation;
				this.randomAns = this.lists[randomIndex2].word;
					
				if(this.userAnswer2){
					this.userAnswer2='';
				}
				if(this.giveBack2){
					this.giveBack2='';
				}
			},
			checkAnswer2(){
				if(this.userAnswer2===this.randomAns){
					this.clickBtm2();
					this.score++;
				}else{
					this.giveBack2='no'
				}
			},
			touchStart(e){
					this.startX=e.touches[0].clientX;
			},
			touchMove(){
				
			},
			touchEnd(e){
				this.endX=e.changedTouches[0].clientX;
				if(this.startX-this.endX>this.threshold){
					uni.navigateTo({
						url:'/pages/tabbar/tabbar4_1/tabbar4_1'
					})
				}else if(this.startX-this.endX<-this.threshold){
					this.clickBtm2();
				}
			},
			ChooseWord(){
				uni.navigateTo({
					url:'/pages/tabbar/tabbar4_1/tabbar4_1'
				})
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
		margin-top: 200upx;
		posing: relative;
	}
	.inputCon{
		background-color: red;
	}
	.textForm{
		text-align: center;
		margin-left:200rpx;
	}
</style>
	
