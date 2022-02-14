<template>
	<div class="app">
		<div id="nav">
			<router-link to="/sign-up"> Sign Up </router-link>
			<router-link to="/log-in"> Log In </router-link>
			<router-link to="/music"> Music </router-link>
			<!-- <router-link to="/playlists"> Playlists </router-link> -->
		</div>
		<router-view />
	</div>
</template>

<script>
import axios from 'axios';

export default {
	name: 'App',
	beforeCreate() {
		this.$store.commit('initializeStore');

		const token = this.$store.state.token;

		if (token) {
			axios.defaults.headers.common['Authorization'] = 'Token ' + token;
		} else {
			axios.defaults.headers.common['Authorization'] = '';
		}
	},
};
</script>

<style>
#app {
	font-family: 'Luckiest Guy', cursive;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	background-color: rgba(92, 109, 184, 0.386);

	letter-spacing: 5px;
	text-align: center;
	color: #15e3ac;
	margin-top: 60px;
}

#nav {
	color: #15e3ac;

	/* display: inline; */
	font-family: 'Luckiest Guy', cursive;
	/* position: relative; */
	margin-top: 10px auto;
	text-align: left;
	min-height: 10vh;
	display: flex;
	flex-direction: column;
	padding: 60px;
	font-size: 30px;
	text-decoration: none;
}
</style>
