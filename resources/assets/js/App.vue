<template>
	<div class="container">
		<div class="navbar">
			<div class="navbar__brand">
				<router-link to="/">Recipe Box</router-link>
			</div>

			<ul class="navbar__list">
				<li class="navbar__item" v-if="!check">
					<router-link to="/login">LOGIN</router-link>
				</li>
				<li class="navbar__item" v-if="!check">
					<router-link to="/register">REGISTER</router-link>
				</li>
				<li class="navbar__item" v-if="check">
					<router-link to="/recipes/create">CREATE</router-link>
				</li>
				<li class="navbar__item" v-if="check">
					<a href="#" @click.stop="logout">LOGOUT</a>
				</li>
			</ul>
		</div>

		<div class="flash flash__success" v-if="flash.success">
			{{ flash.success }}
		</div>

		<div class="flash flash__error" v-if="flash.error">
			{{ flash.error }}
		</div>

		<router-view></router-view>
	</div>
</template>

<script type="text/javascript">
	
	import Flash from './helpers/flash'
	import Auth from './store/auth'
	import { post } from './helpers/api'

	export default {
		created() {
			Auth.initialize()
		},
		data() {
			return {
				flash: Flash.state,
				auth: Auth.state
			}
		},
		computed: {
			check() {
				return this.auth.api_token && this.auth.user_id
			}
		},
		methods: {
			logout() {
				post('/api/logout')
					.then( res => {
						if (res.data.logged_out) {
							Auth.remove()
							Flash.setSuccess('Bye!')
							this.$router.push('/login')
						}
					})
					.catch( err => {

					})
			}
		}
	}

</script>