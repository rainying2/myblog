<template>
	<!--父子组件传值传值把数据传过去的，文章会自动全部显示-->
	<all-article :passages="passages" :type="type"></all-article>
</template>

<script>
	import allArticle from '../../components/allArticle'
	import api from '@/fetch/api'
	export default{
		name:'tech',
		components:{
			allArticle,
		},
		data(){
			return{
				passages:[
					
//					模板
//					{title:'我不是药神--来，吃个橘子吧',time:'2020-6-25',breif:`<p>我读大学时，有一次去医院检查身体。从诊室出来，看见一个三十多岁的女人蹲在地上，捂着肚子嚎啕大哭。“怎么办啊！去哪儿弄这么多钱啊！”哭声尖锐如一把刀，似要撕裂身体。貌似她丈夫的男人把诊断书攥成一团，一边摩挲女人的后背一边抹泪，讲不出一句安慰的话。</p><p>我晃晃悠悠走出医院，双腿软得像踩了棉花，恐惧、同情、忧愤等情绪在心中冲撞。从那时起，我才近距离体会到，原来世上真的有一群人在眼睁睁地等死，眼睁睁看着自己的生命因贫穷而耗竭。</p><p>《我不是药神》将我当时的情绪再度诱发出来。王砚辉饰演的假药贩子张长林说：“这个世界上只有一种病，穷病。”在物质极其充裕的时代，穷能限制想象力，穷能扼杀多种选择，“穷”不再是形容词，而是变成了一个名词和一个标签。穷，就是原罪。</p><p>剧情不算复杂。徐峥饰演的程勇原本是个彻头彻尾的loser，前妻因难忍家暴而离婚，唯一的儿子将跟随母亲出国生活，自己没有一技之长只好靠卖印度神油为生，结果生意冷清，连租金都成了问题。机缘巧合下，他认识了王传君扮演的慢粒白血病患者吕受益，于是做起了从印度走私仿制药的生意。初衷当然是为了赚钱，但因为仿制药价格远远低于国内正版药，无心插柳竟救了不少人命。</p><p>`},
//					{title:'阿甘正传--飘飞的羽毛',time:'2020-6-25',breif:`&nbsp;&nbsp;&nbsp;&nbsp;常常和朋友们谈起阿甘。阿甘太运气了！朋友们总是这样说。我哑然。我很奇怪，阿甘坐在那张凳子上，难道只是在告诉来来往往的陌生人：“瞧，我多运气”？<br>&nbsp;&nbsp;&nbsp;&nbsp;在好些年前，我曾对人生充满困惑。我不知道人活着为什么。有时候，我坐在窗台上，对自己说：我现在跳下去，与我活到死相比也没有区别吧。幸好，我没有跳下去。整整想了两年，我想出了一个答案：人怎么样才能活得更好？这个问题虽然没有答案，但心里不已经没有先前那么迷茫。<br>&nbsp;&nbsp;&nbsp;&nbsp;为什么要说这个事呢？因为在看这部片子的时候，我似乎又一次体验了那个追问人生的过程。<br>&nbsp;&nbsp;&nbsp;&nbsp;一个正常的人，拥有判断能力，他知道什么是重要的，什么是不重要的。一个正常的人，可以有很多选择，所以总是在等待时机。一个正常的人，不会把精力浪费在没有用的地方。但阿甘偏偏不是个正常人，他的智商比普通人低，他甚至差点就进了智障学校。女朋友、学校球队、部队、乒乓、养虾、跑步，似乎他的一切都不是自己在选择，而是别人在选择。当然，他也不会去问“人生是什么”之类的问题。他只会傻傻地去做一件件的事情。<br>&nbsp;&nbsp;&nbsp;&nbsp;这个故事到底想说的是什么？我觉得，导演就是用一种非常极端的方式，说了一个道理：选择很可能误导人生。因为选择太多，有的人没有用心地做事，这种态度进一步影响了他的人生。面对人生，或许应该有这种准备：“人生就像一盒巧克力，你不知道会选中哪一颗”。<br>`},
				],
				type:{
					title:'技术文章',
					describe:'这是技术文章的简介'
				}
			}
		},
		mounted(){
			api.categoryArticleFront(this.type.title).then(res=>{
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
			})
		},
		methods:{
			parseTags(){
				let reg=/<img src/g;
				this.passages.forEach(element => {
					element.tags=element.tags.split(',');
					element.summary=element.summary.replace(reg,`<img data-src`);
				});
			}
		},
		
	}
</script>

<style scoped lang="less">

</style>