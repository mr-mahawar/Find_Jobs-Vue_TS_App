<template>
	<div class="app">
		<transition name="fade">
			<div class="tip" v-if="!tipHidden">
				Hover a Job for more description...
			</div>
		</transition>
		<h1 class="logo">Find Jobs</h1>
		<div class="order-container">
			<h3>Order by :</h3>
			<div class="order-buttons">
				<button @click="changeOrder('title')">Title</button>
				<button @click="changeOrder('location')">Location</button>
				<button @click="changeOrder('salary')">Salary</button>
			</div>
		</div>
		<job-list :jobs="jobs" :order="order"></job-list>
	</div>
</template>

<script lang="ts">
	import { defineComponent, reactive, ref, onMounted } from "vue";

	import Job from "./types/Job";
	import OrderTerm from "./types/OrderTerm";

	import JobList from "./components/JobList.vue";

	export default defineComponent({
		name: "App",
		components: {
			JobList,
		},

		setup() {
			const jobs = reactive<Job[]>([
				{
					title: "full stack developer",
					location: "delhi",
					salary: 45000,
					id: "1",
				},
				{
					title: "front end developer",
					location: "mumbai",
					salary: 30000,
					id: "2",
				},
				{
					title: "backend developer",
					location: "kolkata",
					salary: 40000,
					id: "3",
				},
				{
					title: "ui / ux developer",
					location: "bangalore",
					salary: 35000,
					id: "4",
				},
				{
					title: "graphic designer",
					location: "chennai",
					salary: 21000,
					id: "5",
				},
				{
					title: "video editor",
					location: "jaipur",
					salary: 32000,
					id: "6",
				},
				{
					title: "Photoshop Expert",
					location: "ahmadabad",
					salary: 22000,
					id: "7",
				},
				{
					title: "Digital Marketing Manager",
					location: "patna",
					salary: 23000,
					id: "8",
				},
			]);

			onMounted(() => {
				setTimeout(() => {
					tipHidden.value = false;
					setTimeout(() => {
						tipHidden.value = true;
					}, 7000);
				}, 2000);
			});

			const tipHidden = ref<boolean>(true);

			const order = ref<OrderTerm>("title");

			const changeOrder = (term: OrderTerm) => {
				order.value = term;
			};

			return { jobs, order, changeOrder, tipHidden };
		},
	});
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Nunito+Sans&display=swap");
	@import url("https://fonts.googleapis.com/css2?family=Staatliches&display=swap");

	* {
		box-sizing: border-box;
		font-family: "Nunito Sans", sans-serif;
	}

	body {
		margin: 0;
		min-height: 100vh;
		background-color: #63a4ff;
		background-image: linear-gradient(315deg, #63a4ff 0%, #83eaf1 74%);
	}

	.tip {
		position: fixed;
		background-color: white;
		bottom: 20px;
		right: 20px;
		padding: 10px;
		border: 3px solid dodgerblue;
		border-radius: 4px;
	}

	h1.logo {
		font-family: "Staatliches", cursive;
		text-align: center;
		font-size: 5rem;
		color: dodgerblue;
		letter-spacing: 10px;
	}

	.order-container {
		max-width: 800px;
		margin: 0 auto;
		border: 3px solid dodgerblue;
		border-radius: 7px;
		padding: 0px 25px 25px 25px;
		background-color: rgba(255, 255, 255, 0.25);
		backdrop-filter: blur(5px);
		transition: 0.5s;
	}

	.order-container:hover {
		background-color: rgba(255, 255, 255, 0.4);
	}

	.order-buttons {
		display: flex;
		justify-content: space-evenly;
	}

	.order-buttons button {
		outline: none;
		border: 2px solid dodgerblue;
		border-radius: 4px;
		background-color: white;
		font-size: 1rem;
		font-weight: bold;
		padding: 5px;
		min-width: 120px;
		box-shadow: 0 2px 5px rgba(128, 128, 128, 0.5);
		cursor: pointer;
		transition: 0.3s;
	}

	.order-buttons button:hover {
		transform: translateY(-2px);
		box-shadow: 0 2px 5px rgba(128, 128, 128, 0.75);
		background-color: dodgerblue;
		color: white;
	}

	.order-buttons button:active {
		transform: translateY(0px);
	}

	.fade-enter-active,
	.fade-leave-active {
		transition: opacity 0.2s ease;
	}

	.fade-enter-from,
	.fade-leave-to {
		opacity: 0;
	}

	@media screen and (max-width: 800px) {
		h1.logo {
			font-size: 4rem;
		}

		.order-container {
			width: 95%;
		}

		.order-buttons button {
			min-width: 85px;
			padding: 3px;
		}
	}
</style>
