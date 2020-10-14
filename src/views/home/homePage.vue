<template>
		<!--父子组件传值传值把数据传过去的，文章会自动全部显示-->
		<all-article :passages="passages" :type="type"></all-article>
</template>

<script>
	import allArticle from '../../components/allArticle'
	import api from '@/fetch/api'

	export default{
		name:'homePage',
		components:{
			allArticle,
		},
		data(){
			return {
				passages:[
//					模板
//					{title:'海上钢琴师--俗人理解不了的幸福',time:'2020-6-30',articleId:'1',breif:"关于钢琴，关于尽头，关于彼岸，这些我都不想说。我只想说说1900这个人。<br><br>众人叫他天才，众人为之疯狂。1900，从拥有这个不平凡的名字起，就注定是个不平凡的人。目光、掌声和荣耀，平凡人可能终其一生都得不到的东西，对于天才的1900就像空气一样稀松平常。<br>但目光、掌声和荣耀并不能令人幸福，也不长久。<br>电影里有一个镜头让我特别难受：人们围绕在1900身边为音乐起舞的时候，有人看见了自由女神，一下子所有的人呼啦啦作鸟兽散，只剩下1900孤寂的身影。再多的荣耀也挽救不了孤独，此刻他非天才，是个可怜的被遗弃者。<br><br>天才其实是世界上最不幸的人。所有的天才都是异类。而再体面的异类都不会被人真正地爱。那些为1900的琴声瞠目结舌的人，在琴声终结的时候，他们也就咂巴着嘴散去。1900这样的天才更像是个宠物。人们会喜欢它、呵护它、痴迷它，但它跑到马路中间迎面驰来飞车，谁也不会扑过去用自己的身体挡住。"},
//					{title:'蝴蝶效应--无可奈何的选择',time:'2020-6-30',articleId:'2',breif:`很偶然地看到一个关于电影《The Butterfly Effect》（《蝴蝶效应》）的帖子，介绍影片有几个版本的不同结局，很有些意味；重新勾起了我对这部电影的感触。<br>It has been said that something as small as the flutter of a butterfly’s wing can ultimately cause a typhoon halfway around the world.                                          -Chaos Theory<br>这是混沌理论中最通俗、也最为人所知的表达了，“蝴蝶效应”的提法最初出自1972年美国麻省理工学院教授、混沌学开创人之一E.N.洛伦兹在美国科学发展学会第139次会议上的论文：“巴西丛林一只蝴蝶偶然扇动翅膀，可能会在美国得克萨斯州掀起一场龙卷风”。一个混沌系统是无法预言、操纵和控制的，而且对于系统的初始条件具有极端敏感的依赖性，在系统初始任何一点点细微的改变，都会在系统后期发生翻天覆地的变化……<br>埃文在发现自己可以通过阅读过去的日记回到那个时间点、并找回失去的记忆时，为了得到最理想的现在，他一次次地回到过去，可是每一次的改变都是“猜到了开始，没有猜到结局“：记起了对凯莉的爱，凯莉却间接地因此而死亡；和凯莉成为了恋人，却杀死了她的弟弟；解救了小狗，却使得伦尼杀死了汤米而被关进精神病院，凯莉也内疚地堕落成吸毒的妓女；救了塞姆普太太和她的孩子，自己却成了残疾，伦尼和凯勒则成了幸福的一对儿……每一次的追回时间都以为可以通过已知的结局改变最终的“现在”，没想到改变的还仅仅只是开始……每一次不甘的闪回，像极了《大话西游》中用月光宝盒拦下自刎的剑；`}
				],
				type:{
					title:'所有文章',
					describe:'这是所有文章的简介'
				}
			}
		},
		created(){
			api.allArticleFront().then(res=>{
				switch(res.code){
					case '200':
						console.log('获取文章成功！');
						this.passages=res.data;
						this.parseTags();
						break;
					case '400':
						console.log('服务器开小差了！');
						break;
				}
			},err=>{
				console.log(err);
			});
		},
		methods:{
			//homePage和其他几个music,tech等等的功能有重复
			parseTags(){
				let reg=/<img src/g;
				this.passages.forEach(element => {
					element.tags=element.tags.split(',');
					element.summary=element.summary.replace(reg,`<img data-src`);
				});
			}
		}
	}
</script>

<style scoped lang="less">

</style>
