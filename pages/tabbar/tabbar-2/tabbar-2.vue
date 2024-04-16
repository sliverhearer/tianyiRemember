<template>
	<view class="">
			<view class="wordsForm" v-for="(words,index) in tempList" :key="words.id">
				<button @click="ShowWord(words.id)">{{nihonWord}}</button><text>-- {{words.translation}}</text>
			</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				list:[],
				tempList:[],
				pageSize:50,
				currentPage:1,
				nihonWord:'--'
			}
		},
		created() {
		this.list=require('@/static/nihon.json');
		this.tempList=this.list.slice(0,this.pageSize);
		},
		onReachBottom() {
		    // 当下拉到页面底部时触发  
		    if (this.currentPage * this.pageSize < this.list.length) {
		      this.loadMoreData();
			  console.log(this.currentPage)
		    } else {  
		      uni.showToast({  
		        title: '没有更多数据了',  
		        icon: 'none'  
		      });  
		    }  
		},
		methods: {
		 loadMoreData() {  
		      const start = this.currentPage  * this.pageSize;  
		      const end = (this.currentPage +1)* this.pageSize;  
		      const newData = this.list.slice(start, end);  
		      this.tempList = this.tempList.concat(newData);  
		      this.currentPage++;
		    },
		ShowWord(num){
			this.nihonWord=this.list[num-1].word;
		}
		  }  
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
		margin-top: 200upx;
	}
	.wordsForm{
		text-align: center;
	}
</style>
