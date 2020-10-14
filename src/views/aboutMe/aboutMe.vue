<template>
	<div class="aboutMe">
		<div class="introduce">
			<img class="headImg" src="../../assets/img/myImg.jpg"/>
			<h1>{{this.user.name}}</h1>
			<h2>{{this.user.signature}}</h2>
			<p>{{this.user.breif}}</p>
      <!-- 以下信息均写死，等以后有时间再来填坑 -->
      <div class="info">
        <p style="text-align: left;">学校：&nbsp;&nbsp;&nbsp;&nbsp;仲恺农业工程学院</p>
        <p style="text-align: left;">学号：&nbsp;&nbsp;&nbsp;&nbsp;201710214913</p>
        <p style="text-align: left;">学院：&nbsp;&nbsp;&nbsp;&nbsp;信息科学与技术学院</p>
        <p style="text-align: left;">专业：&nbsp;&nbsp;&nbsp;&nbsp;计算机科学与技术</p>
        <p style="text-align: left;">班级：&nbsp;&nbsp;&nbsp;&nbsp;计算机174班</p>
        <p style="text-align: left;">性别：&nbsp;&nbsp;&nbsp;&nbsp;男</p>
        <p style="text-align: left;">年龄：&nbsp;&nbsp;&nbsp;&nbsp;20</p>
      </div>
			<table class="stack">
				<tr>
					<th width="20%" style="text-align: left;">技术栈</th>
					<th width="25%">了解</th>
					<th width="20%">熟悉</th>
					<th width="20%">熟练运用</th>
					<th width="20%">精通</th>
				</tr>
				<tr v-for="skill in skills">
					<td>{{skill.name}}</td>
					<td colspan="4">
						<transition name="showDegree">
							<div class="degree" :class="[isActive?'':activeClass]"  v-show="showDegree" :style="{width:skill.degree,backgroundColor:skill.color}"></div>
						</transition>
					</td>
				</tr>
				<!--了解 15%，熟悉35%，熟练掌握60%，精通85%-->
			</table>
		</div>
	</div>
</template>

<script>
	import api from '@/fetch/api'
	export default{
		name:'aboutMe',
		data(){
			return{
				user:{
					name:'',
					imgsrc:'',
					signature:'',
					breif:'',
				},
				skills:[
					//了解 16%，熟悉45%，熟练掌握70%，精通85%
					{name:'Html+Css',degree:'70%',color:'orange'},
					{name:'Javascript',degree:'50%',color:'green'},
					{name:'Jquery',degree:'30%',color:'yellow'},
					{name:'Vue',degree:'70%',color:'#cf4647'},
					{name:'Node.js',degree:'45%',color:'#524656'},
					{name:'MySql',degree:'20%',color:'#595b5a'},
					{name:'Java',degree:'40%',color:'red'},
					{name:'Git',degree:'20%',color:'blue'},
				],
				showDegree:false,//展示熟练度条
				isActive:false,//激活发廊滚动条效果
				activeClass:'flow',//激活的class
			}
		},
		mounted(){
			this.showDegree=true;
			api.getMyInfo().then(res=>{
				switch(res.code){
					case '200':
					console.log('获取信息成功');
					this.user=res.data;
					break;
					case '400':
					console.log('服务器炸了，待会儿再请求吧');
					break;
				}
			},err=>{
				console.log(err);
			});
		},
		methods:{
			stopMove(){
				this.isActive=!this.isActive;
			}
		},
	}
</script>

<style scoped lang="less">
	.aboutMe{
		text-align: center;
		padding: 30px;
		.introduce{
			padding: 30px;
			box-sizing: border-box;
			min-height: 100%;
			background: white;
			.headImg{
				border-radius: 50%;
				width: 190px;
			}
			h1{
				font-size:25px ;
				margin-top:10px;
			}
			h2{
				font-size: 18px;
				font-weight: normal;
			}
			p{
				font-size: 16px;
				max-width: 500px;
				margin:20px auto;
			}
		}
    .info{
      position: absolute;
      margin:10px 320px 20px;
      width: 400px;
      height: 450px;
      border-right: 1px solid #cbcbcb;
      p{
        margin-left: 60px;
        font-size: 22px;
      }
    }
		.stack{
			width:40%;
			margin:40px 800px 20px;
			text-align: left;
			th{
				text-align: center;
			}
			tr{
				height:50px;
				line-height: 50px;
				font-size: 16px;
				td{
					vertical-align: middle;
					overflow: hidden;
					position: relative;
				}
			}
			.degree{
				height: 30px;
				margin:auto 0;
				overflow: hidden;
				background-size: 50px 50px;
				// background-image: linear-gradient( 135deg,transparent,transparent 25%, rgba(255,255,255,0.8) 25%, rgba(255,255,255,0.8) 50%,transparent 50%,transparent 75%,rgba(255,255,255,0.8) 75%, rgba(255,255,255,0.8) 100% );

			}
			.flow{
				animation: degreeMove 1s linear infinite;
			}
			/*控制技能表运动的css*/
			.showDegree-enter-active {
				transition: all 2s ease;
			}
			.showDegree-leave-active {
				transition: all 2s ease;
			}
			.showDegree-enter, .showDegree-leave-to{
				transform: translateX(-100%);
				opacity: 0;
			}

			@keyframes degreeMove{
				0{}
				100%{
					background-position:100px 0;
				}
			}
		}
		.stop{
			width:120px;
			height: 40px;
			cursor: pointer;
			border:1px solid;
			border-radius: 5px;
			background: #d9534f;
			color: white;
		}
}

@media screen and (max-width: 900px) {
	.aboutMe{
		padding: 30px 0;
		.introduce{
			padding:30px 10px;
		}
		.stack{
			width: 100%;
			tr,td{
				font-size: 0.5rem;
			}
		}
	}
}

</style>
