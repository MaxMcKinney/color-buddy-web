<template>
	<div class="palette-card">
		<span class="palette-card-title">{{title}}</span>
		<ul class="palette-card-colors">
			<!-- For each color item in the color array use it's value to create a new list item
			with the color background from the list item -->
			<palette-card class="palette-color" v-for="(palette, index) in paletteIds" :key="index" :title="palette.title" :colors="fetchPaletteColors(palette)"></palette-card>
		</ul>
	</div>
</template>

<script>
import firebase from './firebaseInit'
import paletteCard from './PaletteCard'

export default {
	name: 'group-card',
	data() {
		return {

		}
	},
	props: {
		title: String,
		paletteIds: Array,
	},
	components : {
		'palette-card' : paletteCard
	},
	methods : {
		fetchPaletteColors(paletteId) {
			firebase.firestore().collection('colorPalettes').doc(paletteId).get().then(palette => {
				return palette.colors;
			});
		}
	}
}
</script>

<style scoped>
.palette-card {
	width: 100%;
	height: 110px;
	border-radius: 16px;
    overflow: hidden;
	position: relative;
	transition: all 0.3s;
}
.palette-card:hover, .palette-card:focus, .palette-card:active {
	box-shadow: 0px 8px 23px #0000001a;
	transform: translateY(-2px);
	cursor: pointer;
}
.palette-card-title {
	color: #1E1E1E;
	font-family: Lato;
	font-size: 13px;
	font-weight: bold;
	padding: 4px 12px;
	background: white;
	border-radius: 8px;
	position: absolute;
	top: 12px;
	left: 16px;
}
.palette-card-colors {
	list-style: none;
	margin: 0;
	padding: 0;
	width: 100%;
	height: 100%;
	display: flex;
}
.palette-color {
	height: 100%;
	width: 100%;
	display: inline-block;
}
</style>
