<template>
	<div class="container">
		<div class="navbar">
			<div class="navbar__brand">
				<router-link to="/">Recipe Box</router-link>
			</div>

			<ul class="navbar__list">
				<li class="navbar__item">
					<router-link to="/login">LOGIN</router-link>
				</li>
				<li class="navbar__item">
					<router-link to="/register">REGISTER</router-link>
				</li>
				<li class="navbar__item">
					<router-link to="/logout">LOGOUT</router-link>
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

	export default {
		data() {
			return {
				flash: Flash.state
			}
		}
	}

</script>