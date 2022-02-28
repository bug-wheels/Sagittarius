<template>
	<el-container>
<!--		<el-header style="height: 60px;">-->
<!--			<el-row>-->
<!--				<el-col :span="8">-->
<!--					<img src="@/assets/logo.png" width="100px" style="padding-top:10px; padding-left:20px;">-->
<!--				</el-col>-->
<!--			</el-row>-->
<!--		</el-header>-->
		<el-main>
			<el-row :gutter="12">
				<el-col :span="3" class="card" v-for="link in links" :key="link.name">
					<el-card shadow="hover">
						<el-link :href="link.url" target="_blank">{{ link.name }}</el-link>
					</el-card>
				</el-col>
			</el-row>
			<el-row :gutter="20" class="margintop10">
				<el-col :span="4" v-for="sou in sources" :key="sou.name" class="margintop10">
					<el-card :body-style="{ padding: '0px' }" >
						<img
								:src="sou.img"
								class="image"
						/>
						<div style="padding: 14px">
							<span>{{ sou.name }}</span>
							<div class="bottom">
								<time class="time">{{ sou.publishTime }}</time>
								<el-button type="text" class="button" @click="showSourceInfo = sou; showSource = true">{{ sou.score }}</el-button>
							</div>
						</div>
					</el-card>
				</el-col>
			</el-row>
		</el-main>
		<el-drawer
				v-model="showSource"
				:title="showSourceInfo.name"
				direction="rtl"
				size="50%"
		>
			<el-image
					style="width: 100%; max-height: 300px"
					:src="showSourceInfo.img"
					:preview-src-list="showSourceInfo.imgArr"
					fit="cover"
			/>
			<div class="margintop10">
				{{ showSourceInfo.description}}
			</div>
			<div class="margintop10">
				标签：
				<el-tag class="mx-1" type="info" effect="dark" v-for="la in showSourceInfo.label">{{ la }}</el-tag>
			</div>

			<div class="margintop10">
				相关资源：
				<el-button v-show="showSourceInfo.bdyp" @click="showSourceDialogVisible = true; showSourceDialogMessage = showSourceInfo.bdyp" type="primary">百度网盘</el-button>
				<el-button v-show="showSourceInfo.aliyp" type="success">阿里云盘</el-button>
				<el-button type="info">其他</el-button>
				<el-button type="warning">Warning</el-button>
				<el-button type="danger">Danger</el-button>
			</div>
		</el-drawer>
		<el-dialog
				v-model="showSourceDialogVisible"
				title="Good Luck"
				width="30%"
		>
			<span>{{ showSourceDialogMessage }}</span>
		</el-dialog>
		<el-footer>&copy; 2022 - Present
			<el-link class="pull-right font-color-gold">开源协议</el-link>
			<el-link class="pull-right">关于</el-link>
		</el-footer>
	</el-container>
</template>

<script>
export default {
	data() {
		return {
			showSource: false,
			showSourceDialogVisible: false,
			showSourceDialogMessage: '',
			showSourceInfo: {},
			restaurants: [],
			timeout: null,
			search_text: '',
			currentYear: new Date().getFullYear(),
			links: [
				{name: 'Teambition', url: 'https://www.teambition.com/projects'},
				{name: '同盾', url: 'https://logintest.tongdun.cn'},
				{name: '商汤', url: 'https://v2-devcenter.visioncloudapi.com/#/doc/v2/index'},
				{name: '身份证号码生成器', url: 'http://sfz.uzuzuz.com'},
			],
			sources: [
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png'],
					description: 'ddfasdfeadf',
					bdyp: 'sfeasdfeadsfefadf',
					label: ['Netty', 'RPC', 'Java']
				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']
				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				},
				{
					name: 'Netty 核心原理剖析与 RPC 实践',
					publishTime: '2022年02月25日',
					score: '7.5',
					img: 'https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png',
					imgArr: ['https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png']

				}
			]
		}
	},
	methods: {},

}
</script>

<style scoped>
.mx-1 {
	margin-left: .25rem;
	margin-right: .25rem;
}
.time {
	font-size: 13px;
	color: #999;
}

.bottom {
	margin-top: 13px;
	line-height: 12px;
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.button {
	padding: 0;
	min-height: auto;
}

.image {
	display: block;
	width: 100%;
	height: 100px;
}


.card {
	margin-top: 10px;
	text-align: center;
}

.el-container {
	height: 100%;
}

.el-header {
	height: 60px;
	background-color: #000000;
	line-height: 60px;
}

.el-header > span,
.el-header .el-dropdown {
	font-size: 18px;
}

.el-footer {
	background-color: #252d36;
	color: #ffc852;
	text-align: center;
	line-height: 60px;
}

.el-main {
	color: #333;
}
</style>
