<template>
	<view class="content" @touchstart="touchStart" @touchend="touchEnd" @touchmove="touchMove" >
		<view>
			<text>{{score}}</text>
			<button @click="ChooseAns()">获得问题</button>
			<view class="" >
				{{question}}
			</view>
			<button @click="checkAns(0)" >{{queList[0]}}</button>
			<button @click="checkAns(1)" >{{queList[1]}}</button>
			<button @click="checkAns(2)" >{{queList[2]}}</button>
			<button @click="checkAns(3)" >{{queList[3]}}</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				startX:'',
				endx:'',
				threshold:'',
				localWord:[],
				question:'',
				realAns:'',
				queList:[],
				score:''
			}
		},
		onLoad(){
			this.localWord=require('../../../static/nihon.json');
			uni.getStorage({
				key:'score',
				success:function(res){
					this.score=res.data;
					console.log("success");
				}
			})
			
		},
		methods: {
			touchStart(e){
					this.startX=e.touches[0].clientX;
			},
			touchMove(){
				
			},
			touchEnd(e){
				this.endX=e.changedTouches[0].clientX;
				if(this.startX-this.endX<-this.threshold){
					uni.navigateTo({
						url:'pages/tabbar/tabbar-4/tabbar-4'
					})
				}
			},
			ChooseAns(e){
				this.getRandomQue();
				this.getRandomAns();
			},
			getRandomQue(){
				const randomIndex=Math.floor(Math.random()*this.localWord.length);
				//this.localWord.splice(randomIndex,1);
				this.question=this.localWord[randomIndex].word;
				this.realAns = this.localWord[randomIndex].translation;
			},
			getRandomAns(){
				const randomIndex1=Math.floor(Math.random()*this.localWord.length);
				//this.localWord.splice(randomIndex1,1);
				const randomIndex2=Math.floor(Math.random()*this.localWord.length);
				//this.localWord.splice(randomIndex2,1);
				const randomIndex3=Math.floor(Math.random()*this.localWord.length);
				//this.localWord.splice(randomIndex3,1);
				this.queList
				= [this.localWord[randomIndex1].translation,this.localWord[randomIndex2].translation,
				this.localWord[randomIndex3].translation,this.realAns];
				this.queList.sort(()=>Math.random()-0.5);
			},
			checkAns(num){
					if(this.queList[num]==this.realAns){
					uni.showToast({
						title:'回答正确',
						icon:'none'
					});
					this.getRandomQue();
					this.getRandomAns();
					this.score++;
					var i = this.score;
					uni.setStorage({
						key:'score',
						data:i,
						success:function(res){
							console.log("成功");
							}
					})
				}else{
					uni.showToast({
						title:'回答错误',
						icon:'none'
					})
				}
			}
		}
	}
</script>

<style>

</style>
