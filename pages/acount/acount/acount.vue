<template>
	<view>
		<input type="number" v-model="Num"/>
		<button @click="count">计算</button>
		{{moneySum}}
		<button @click="save">保存</button>
		<button @click='get'>获得</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money:0,
				Num:0,
				moneySum:0
			}
		},
		onload(){
			
		},
		methods: {
			count(){
				let mo = Number(this.moneySum);
				let num = Number(this.Num);
				this.moneySum=mo+num;
			},
			save(){
				uni.setStorage({
					key:'mon',
					data:this.moneySum,
					success:function(){
					
						console.log("success")
				}
			})
			},
			get(){
				uni.getStorage({
				key:'mon',
				success:function(res){
					this.moneySum=res.data;
					console.log(res.data)
			}
		})
	}
}
}
</script>

<style>

</style>
