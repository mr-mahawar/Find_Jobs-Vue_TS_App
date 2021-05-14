<template>
	<div class="app">
		Hello TS Vue 3 APP
		<br />
		Name : {{ name }}
		<!-- +state.name -->
		<br />
		Age: {{ age }}
		<!-- +state.age -->
		<br />
		<button @click="changeName('Dahi Vada')">Change Name</button>
		<button @click="changeAge(26)">Change Age</button>
	</div>
</template>

<script lang="ts">
	import { defineComponent, ref } from "vue"; // +reactive

	export default defineComponent({
		name: "App",
		components: {},

		setup() {
			// const state = reactive({
			// 	name: "Tilak Mahawar",
			// 	age: 22 as number | string,
			// });

			const name = ref<string>("Tilak Mahawar");
			const age = ref<number | string>(22);

			const changeName = (uName: string) => {
				// state.name = uName;
				name.value = uName;
			};

			const changeAge = (uAge: number | string) => {
				// state.age = uAge;
				age.value = uAge;
			};

			return { name, age, changeName, changeAge }; // + state
		},

		// data() {
		// 	return {
		// 		name: "Tilak Mahawar",
		// 		age: 22 as number | string,
		// 	};
		// },

		methods: {
			// changeName(name: string) {
			// 	this.name = name;
			// },
			// changeAge(age: number | string) {
			// 	this.age = age;
			// },
		},
	});
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");

	* {
		box-sizing: border-box;
	}

	body {
		margin: 0;
		min-height: 100vh;
		font-family: "Montserrat", sans-serif;
	}
</style>
