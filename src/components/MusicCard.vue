<template>
	<div>
		<div class="card music-card">
			<div class="image-wrapper">
				<!-- Image Goes Here -->
				<img :src="music.image[4]['#text']" />
			</div>
			<div class="info-wrapper flex-col">
				<!-- Music Name Goes Here -->
				<h3>{{ music.name }}</h3>
			</div>
		</div>
	</div>
</template>
<!-- @click="selectMusic(music.name)" -->
<script>
export default {
	name: 'MusicCard',

	props: ['music'],
	// chartMusic: [],
	// playlists: {}
	methods: {
		selectMusic(musicName) {
			this.$emit('selectMusic', musicName);
		},
	},
};
</script>
