<template>
	<div class="account">
		<div class="main banxin">
			<div class="aside">
				<div class="name">账户名称</div>
				<div class="line"></div>
				<ul class="list">
					<li :class="['item', {'active': selected_id == item.id}]" v-for="item in aside_list" @click="selectType(item.id, item.type)">{{item.name}}</li>
				</ul>
			</div>
			<div class="content">
				<div class="title">{{aside_list[selected_id - 1].name}}</div>
				<div class="wrap">
					<!-- 其实这里可以通过控制组价名称来渲染对应组件内容 -->
					<div class="type-cont" v-show="selected_id == 1">
					</div>
					<div class="type-cont" v-show="selected_id == 2">
					</div>
					<div class="type-cont" v-show="selected_id == 3">
					</div>
					<div class="type-cont" v-show="selected_id == 4">
					</div>
					<div class="type-cont" v-show="selected_id == 5">
					</div>
					<div class="type-cont" v-show="selected_id == 6">
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				aside_list: [
					{
						type: "order_list",
						name: "我的订单",
						id: 1,
					},
					{
						type: "address",
						name: "收货地址",
						id: 2
					},
					{
						type: "message",
						name: "消息通知",
						id: 3
					},
					{
						type: "money",
						name: "资金管理",
						id: 4
					},
					{
						type: "account_set",
						name: "账号设置",
						id: 5
					},
					{
						type: "coupon",
						name: "优惠券",
						id: 6
					},
				],
				selected_id: 1,
			}
		},
		methods: {
			// 点击左侧栏:
			selectType: function(id, type) {
				this.selected_id = id
				this.$router.push({
					path: "/account/"+type
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	$highlight: #32c057;

	.account {
		padding: 40px 0 100px;

		.main {
			display: flex;

			.aside {
				width: 200px;
				height: 380px;
				border: 1px solid #ebeef5;
				padding: 20px;
				text-align: center;
				border-radius: 4px;

				&:hover {
					box-shadow: 0 2px 2px 1px #ebeef5;
				}

				.name {
					line-height: 60px;
					font-size: 16px;
				}
				.line{
					width: 80px;
					margin: 0 auto;
					border-bottom: 1px solid #ebeef5;
				}
				.list {
					line-height: 40px;
					margin: 10px 0;
					font-size: 14px;
					
					.item {
						cursor: pointer;
						&.active {
							color: $highlight;
						}
					}
				}
			}

			.content {
				flex: 1;
				margin-left: 30px;
				.title{
					font-size: 26px;
					line-height: 58px;
				}
				.wrap{
					.type-cont {
						min-height: 300px;
					}
				}
			}
		}
	}
</style>
