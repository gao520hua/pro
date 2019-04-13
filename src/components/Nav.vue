<template>
	<div class="navigator">
		<div class="cont">
			<div class="nav">
				<div class="logo" @click="goHome">
					<img src="../assets/logo.png" alt="">
				</div>
				<ul class="list">
					<li :class="['item', {active: item.path == current_path}]" v-for="item in nav_list">
						<router-link class="link" :to="item.path">{{item.name}}</router-link>
					</li>
				</ul>
			</div>
			<div class="right-wrap">
				<div class="btn register" @click="goRegister">注册</div>
				<div class="btn login" @click="goLogin">登录</div>
				<div class="switch">
					<span :class="['lan', {'active': 1 == language_id}]" @click="swicthLanguage(1)">English</span> /
					<span :class="['lan', {'active': 2 == language_id}]" @click="swicthLanguage(2)">中文</span>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data() {
			return{
				nav_list: [
					{name: "首页", path: "/"},
					{name: "矿机", path: "/product"},
					{name: "关于", path: "/about"}
				],
				current_path: "/",
				languages: [
					{name: 'English', id: 1},
					{name: '中文', id: 2}
				],
				language_id: 2, // 默认语言
			}
		},
		mounted: function() {
			this.current_path = this.$route.path
			if (this.$route.path.indexOf("/product") != -1) {
				this.current_path = "/product"
			}
		},
		watch: {
			$route(to, from) {
				this.current_path = to.path
				if (to.path.indexOf("/product") != -1) {
					this.current_path = "/product"
				}
			}
		},
		methods: {
			goHome: function() {
				this.$router.push({
					path: "/"
				})
			},
			// 前往注册:
			goRegister: function() {
				this.$router.push({
					path: "/register"
				})
			},
			// 前往登录:
			goLogin: function() {
				this.$router.push({
					path: "/login"
				})
			},
			// 切换语言:
			swicthLanguage: function(id) {
				this.language_id = id
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	$highlight: #32c057;
	.navigator{
		background: #f9f9fa;
		font-size: 16px;
		.cont{
			display: flex;
			justify-content: space-between;
			height: 100px;
			line-height: 100px;
			width: 1200px; // 版心宽度
			margin: 0 auto;
			.nav{
				display: flex;
				.logo{
					width: 215px;
					font-size: 0;
					margin-right: 100px;
					cursor: pointer;
				}
				.list{
					display: flex;
					.item{
						margin-right: 10px;
						&.active{
							.link{
								color: $highlight;
							}
						}
						.link{
							display: block;
							padding: 0 18px;
						}
					}
				}
			}
			.right-wrap{
				display: flex;
				align-items: center;
				position: relative;
				.btn{
					height: 34px;
					line-height: 32px;
					padding: 0 20px;
					border: 1px solid #ccc;
					background: #fff;
					border-radius: 4px;
					cursor: pointer;
				}
				.register{
					margin-right: 10px;
					border-color: $highlight;
				}
				.switch{
					position: absolute;
					right: 0;
					top: 4px;
					font-size: 12px;
					line-height: 24px;
					.lan{
						cursor: pointer;
						&.active{
							color: $highlight;
						}
					}
				}
			}
		}
	}
</style>
