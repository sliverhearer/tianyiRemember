<template>
    <view class="content">
        <button @click="showRandomWords">获取随机单词</button>
            <view class="wordsForm" v-for="(words, index) in randomWords" :key="words.id">
                <text>{{ words.word }} -- {{ words.translation }}</text>
            </view>
		<button @click="acount">存钱</button>
    </view>
</template>
<script>
export default {
    data() {
        return {
            allWords: [],
            randomWords: [] ,
			favorites:[]
        };
    },
    onLoad() {
        //this.loadWordsFromFile();
		const tempjson = require('@/static/nihon.json');
		this.allWords = tempjson;
    },  
    methods: {
		acount(){
			uni.navigateTo({
				url:'/pages/acount/acount/acount'
			})
		},
        // loadWordsFromFile() {  
        //     uni.readFile({  
        //         filePath: 'static/nihon.json', // 路径根据你的项目结构进行调整  
        //         success: (res) => {  
        //             try {  
        //                 this.allWords = JSON.parse(res.data);  
        //             } catch (error) {  
        //                 console.error('解析 JSON 失败', error);  
        //             }  
        //         },  
        //         fail: (err) => {  
        //             console.error('读取文件失败', err);  
        //         }  
        //     });  
        // },  
        showRandomWords() {
            if (this.allWords.length < 10) {
                this.randomWords = this.allWords;
            } else {
                const shuffled = this.allWords.slice().sort(() => 0.5 - Math.random());
                this.randomWords = shuffled.slice(0, 10);
            }
        },
    }
};
</script>
<style>
.content {
	/* text-align: center; */
	height: 40upx;
	margin-top: 20upx;
}
.wordsForm{
	text-align: center;
}
</style>
