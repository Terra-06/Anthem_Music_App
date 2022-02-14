<template>
	<div>
		<div class="card music-card">
			<div class="image-wrapper">
				<img :src="music.image[4]['#text']" />
			</div>
			<div class="info-wrapper flex-col">
				<h3>{{ music.name }}</h3>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	name: 'MusicCard',

	props: ['music'],
	methods: {
		selectMusic(musicName) {
			this.$emit('selectMusic', musicName);
		},
	},
};
</script>
