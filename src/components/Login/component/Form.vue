<template>
	<div class="form">
		<el-form label-position="left" label-width="96px" :model="formData">
			<el-form-item :label="labels.label_1">
				<el-input v-model="formData.phone" size="medium">
					<el-select v-model="select_val" slot="prepend" placeholder="请选择" @change="selectChange">
						<el-option :label="item.label" :value="item.val" v-for="item in phone_list">
							<span style="float: left;">{{item.label}}</span>
							<span style="float: right;">{{item.value}}</span>
						</el-option>
					</el-select>
				</el-input>
			</el-form-item>
			<el-form-item :label="labels.label_2">
				<div class="sjyzm">
					<el-input class="yzm-srk" v-model="formData.v_code" size="medium"></el-input>
					<div class="button">发送验证码</div>
				</div>
			</el-form-item>
			<el-form-item label="密码">
				<el-input type="password" v-model="formData.password" size="medium" suffix-icon="el-icon-view">
				</el-input>
			</el-form-item>
			<el-form-item label="确认密码">
				<el-input type="password" v-model="formData.password2" size="medium">
					<span slot="suffix" class="el-input__icon el-icon-view"></span>
				</el-input>
			</el-form-item>
			<el-form-item>
				<el-checkbox v-model="checked">我同意</el-checkbox>
				<a style="color: #5d80b9;" href="">注册服务协议</a>
			</el-form-item>
			<el-form-item>
				<div class="submit">注册</div>
			</el-form-item>
		</el-form>
	</div>
</template>

<script>
	import bus from "@/eventCenter.js"
	
	export default{
		data() {
			return{
				labels: {
					label_1: "手机",
					label_2: "手机验证码"
				},
				formData: {
					phone: "",
					v_code: '',
					password: "",
					password2: "",
				},
				phone_list: [{
						value: "+86",
						label: "中国"
					},
					{
						value: "+82",
						label: "中国1"
					},
					{
						value: "+83",
						label: "中国2"
					},
					{
						value: "+84",
						label: "中国3"
					},
					{
						value: "+85",
						label: "中国4"
					},
					{
						value: "+89",
						label: "中国5"
					},
				],
				select_val: "+86",
				checked: false
			}
		},
		mounted: function() {
			bus.$on("tabChange", val => {
				if (val == "phone") {
					this.labels.label_1 = "手机"
					this.labels.label_2 = "手机验证码"
				} else {
					this.labels.label_1 = "邮箱"
					this.labels.label_2 = "邮箱验证码"
				}
			})
		},
		methods: {
			// 选择不一样的手机号前缀：
			selectChange: function(val) {
				console.log(val)
			}
		}
	}
</script>

<style lang="scss" scoped>
	$highlight: #32c057;
	.form{
		width: 500px;
		margin: 0 auto;
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
</style>
<style lang="scss">
	.el-select .el-input {
		width: 80px;
	}
</style>
