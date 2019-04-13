<template>
	<div class="register">
		<div class="form-box">
			<div class="title">注册</div>
			<div class="content">
				<el-tabs v-model="activeName" @tab-click="handleClick">
					<el-tab-pane label="手机注册" name="first">
						<my-form></my-form>
					</el-tab-pane>
					<el-tab-pane label="邮箱注册" name="second">
						<my-form></my-form>
					</el-tab-pane>
				</el-tabs>
			</div>
		</div>
	</div>
</template>

<script>
	import MyForm from "@/components/Login/component/Form"
	import bus from "@/eventCenter.js"
	
	export default {
		components: {
			MyForm
		},
		data() {
			return {
				activeName: "first",
			}
		},
		methods: {
			// 点击切换：
			handleClick: function(obj) {
				if (obj.name == "first") {
					bus.$emit("tabChange", "phone")
				} else {
					bus.$emit("tabChange", "email")
				}
			},
		}
	}
</script>

<style lang="scss" scoped>
	$highlight: #32c057;
	.register {
		padding: 50px 0;
		.form-box{
			width: 798px;
			margin: 0 auto;
			border: 1px solid #ebeef5;
			box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
			font-size: 14px;
			border-radius: 4px;
			.title{
				height: 46px;
				line-height: 46px;
				background: #f9f9fa;
				padding-left: 20px;
				border-bottom: 1px solid #ebeef5;
			}
			.content{
				width: 500px;
				margin: 50px auto;
				.sjyzm{
					display: flex;
					.yzm-srk{
						width: 180px;
						margin-right: 10px;
					}
					.button{
						width: 100px;
						height: 36px;
						line-height: 34px;
						border: 1px solid $highlight;
						color: $highlight;
						text-align: center;
						border-radius: 4px;
						cursor: pointer;
					}
				}
				.submit{
					width: 300px;
					height: 40px;
					border-radius: 4px;
					text-align: center;
					color: #fff;
					background: $highlight;
				}
			}
		}
	}
</style>
<style lang="scss">
	$highlight: #32c057;
	.el-tabs__nav{
		width: 100%;
		.el-tabs__active-bar{
			background-color: $highlight;
		}
	}
	.el-tabs__item{
		width: 50%;
		&:hover{
			color: $highlight;
		}
		&.is-active{
			color: $highlight;
		}
	}
</style>
