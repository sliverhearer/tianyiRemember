<template>
	<view class="content" >
		<view v-if="ifLoggedIn">
			<view class="">
				你好,{{username}}
			</view>
			<button @click="LoggedOut">注销</button>
		</view>
		<view v-else>
		你怎么知道我喜欢天依	
		{{someData}}
		<input type="text" v-model="username" placeholder="请输入用户名"/>
		<input type="text" v-model="password" placeholder="请输入密码"/>
		<button type="submit" @click="login">登录</button>
		</view>
	</view>
	
</template>

<script>
	export default {
		computed:{
			// this.$store.state.someData
			},
		data() {
			return {
				username:'',
				password:'',
				startX:'',
				endS:'',
				threshold:'',
				acount:[],
				ifLoggedIn:false,
				
			}
		},
		onLoad() {
			this.acount=require('../../../static/acount.json');
		},
		methods: {
			// touchStart(e){
			// 		this.startX=e.touches[0].clientX;
			// },
			// touchMove(){
				
			// },
			// touchEnd(e){
			// 	this.endX=e.changedTouches[0].clientX;
			// 	if(this.startX-this.endX>this.threshold){
			// 		uni.navigateTo({
			// 			url:'/pages/tabbar/tabbar-4/tabbar-4'
			// 		})
			// 	}
			// }
		login(){
		for(var i=0;i<this.acount.length;i++){
		if(this.username==this.acount[i].username&&this.password==this.acount[i].password){
			uni.showToast({
				title:'登录成功',
				icon:'none'
			})
			this.ifLoggedIn=true;
			
		}
	}
	},
		LoggedOut(){
		this.username='';
		this.password='';
		this.ifLoggedIn=false;
		}
	}
}
</script>

<style>
	.container {  
	  display: flex;  
	  flex-direction: column;  
	  align-items: center;  
	  justify-content: center;  
	  height: 100%;  
	}  
	  
	input {  
	  margin-bottom: 10px;  
	  padding: 5px;  
	  width: 90%;  
	}  
	  
	button {  
	  padding: 10px 20px;  
	}
</style>
