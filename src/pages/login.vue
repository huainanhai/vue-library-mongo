<template>
	<div>
		<div class="loginBox" v-if="!userData">
			<h3>LOGIN LIBRARY</h3>
			<div class="inputItem">
				名字：
				<input placeholder="请输入用户名" type="text" v-model="username">
			</div>
			<div class="inputItem">
				密码：
				<input placeholder="密码" type="text" v-model="password">
			</div>
			<div class="loginBtnItem">
				<button @click="loginEvent" class="loginBtn">登录</button>
				<span class="registerBtn">
					<router-link :to="{path: 'register'}">注册</router-link>
				</span>
			</div>
		</div>
		<div class="loginBox" v-else>
			<h3>{{userData.username}}, Congruation on you</h3>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			username: 'wz',
			password: '666',
			userData: null,
		};
	},
	created() {
		// this.getUser();
	},
	methods: {
		loginEvent() {
			this.login();
		},
		getUser() {
			this.dataService.getUser({
				_this: this,
				options: {},
				callback0: res => {
					console.log(res.body.data);
				},
			});
		},
		login() {
			this.userData = null;
			this.dataService.login({
				_this: this,
				options: {
					username: this.username,
					password: this.password,
				},
				callback0: res => {
					const { data } = res.body;
					if (data.code == 102) {
						alert('不存在');
					} else if (data.code == 0) {
						this.userData = data.data;
					}
				},
			});
		},
	},
};
</script>

<style lang="less">
@import '~@less/login.less';
</style>

