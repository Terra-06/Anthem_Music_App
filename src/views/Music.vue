<template>
	<div>
		<div class="music">
			<h1>Music Page</h1>
		</div>

		<div class="search">
			<!-- Search Form Goes Here -->
			<form @submit.prevent="getSearchMusic">
				<input
					type="text"
					:value="searchQuery"
					placeholder="Search Artists"
					@change="handleChange"
				/>

				<button type="submit">Search</button>
			</form>
			<h2>Top Charts</h2>
			<section class="search-results container-grid" v-if="searched">
				<MusicCard
					:music="music"
					:key="music.name"
					v-for="music in searchMusic"
					>{{ music.name }}</MusicCard
				>
			</section>
		</div>
		<!-- @selectMusic="selectMusic" -->

		<div class="genres" v-if="!searched">
			<h2>Playlists</h2>
			<section class="container-grid">
				<MusicGenre
					:genre="genre"
					:key="genre.name"
					v-for="genre in genres"
				/>
			</section>
		</div>
	</div>
</template>

<script>
import axios from 'axios';
import { MUSIC_URL } from '../globals';
const API_KEY = process.env.VUE_APP_MUSIC_API_KEY;
import MusicCard from '../components/MusicCard.vue';

export default {
	name: 'Music',

	components: {
		MusicCard,
	},

	data: () => ({
		genres: [],
		searchQuery: '',
		searchMusic: [],
		searched: false,
	}),

	mounted() {
		this.getSearchMusic();
	},
	methods: {
		async getSearchMusic() {
			const response = await axios.get(
				`${MUSIC_URL}2.0/?method=artist.search&artist=${this.searchQuery}&api_key=${API_KEY}&format=json`
			);
			this.searchMusic = response.data.results.artistmatches.artist;
		},
		handleChange(event) {
			this.searchQuery = event.target.value;
			this.searched = true;
		},
	},
};
</script>

<style>
body {
	background-image: url('../../src/img/speaker.jpeg');
	background-repeat: no-repeat;
	background-size: cover;
}

header {
	background-color: #686a6a33;
	display: flex;
	justify-content: flex-end;
	align-items: center;
	height: 3em;
}

header nav a {
	margin: 0 1em;
}

input {
	background-color: transparent;
	border: 0;
	border-bottom: 2px solid rgba(255, 255, 255, 0.1);
	padding: 0.5em 0.2em;
	width: auto;
	transition: all 0.2s;
	font-size: 1.3rem;
	color: #eee;
}

input:active,
input:focus {
	outline: none;

	border-bottom: 2px solid rgba(255, 255, 255, 0.4);
}

input::placeholder {
	color: rgba(255, 255, 255, 0.5);
	transition: all 0.2s;
}

input:active::placeholder,
input:focus::placeholder {
	color: rgba(255, 255, 255, 0.2);
}

main {
	padding: 2em 0;
}

form {
	width: 100%;
	display: flex;
	justify-content: center;
}

input {
	width: 80%;
	margin: 0 1em;
}

button {
	padding: 0.2em 1em;
	border: 0;
	border-radius: 4px;
	font-size: 1.1rem;
	cursor: pointer;
}

.card {
	max-width: 300px;
	max-height: 380px;
	border-radius: 4px;
	background-color: #585b5e64;
	cursor: pointer;
	transition: all 0.2s;
}

.card:hover {
	opacity: 0.8;
}

.card .image-wrapper {
	width: auto;
}

.card img {
	width: 100%;
	height: 200px;
}

.card .info-wrapper {
	padding: 1em;
}
.container-grid {
	padding: 2em 0;
	display: grid;
	grid-template-columns: repeat(auto-fill, 320px);
	grid-gap: 1em;
	justify-content: center;
}
.genres {
	width: 100%;
}
.genres h2,
.search h2 {
	text-align: center;
}

.music-content .image-container {
	width: 95vw;
	margin: auto;
	border-bottom: 1px solid rgba(255, 255, 255, 0.2);
	padding: 1em 0;
}

.image-container div {
	margin: auto;
	width: 90%;
}

.image-container img {
	margin: auto;
	text-align: center;
	width: 100%;
}

.details {
	width: 80%;
	margin: auto;
}

.flex-row {
	display: flex;
}
.space {
	justify-content: space-between;
}
</style>
