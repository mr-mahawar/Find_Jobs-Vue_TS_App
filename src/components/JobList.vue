<template>
	<div class="job-list">
		<p class="order">Ordered by : {{ order }}</p>
		<transition-group name="list" tag="ul">
			<li v-for="job in orderedJobs" :key="job.id">
				<h2>{{ job.title }}</h2>
				<h4>Location : {{ job.location }}</h4>
				<div class="salary">
					<p>₹ {{ job.salary }} / Month</p>
				</div>
				<div class="description">
					Lorem, ipsum dolor sit amet consectetur adipisicing elit.
					Illo, iusto dicta adipisci sequi possimus iste incidunt
					accusamus sed ullam asperiores saepe at cumque inventore
					ipsum atque hic amet obcaecati nisi minus quia odit
					dignissimos velit. Reiciendis aliquid cumque corrupti
					deserunt quo pariatur officiis obcaecati minima architecto
					incidunt quia, animi modi.
				</div>
			</li>
		</transition-group>
	</div>
</template>

<script lang="ts">
	import { defineComponent, PropType, computed } from "vue";

	import Job from "../types/Job";
	import OrderTerm from "../types/OrderTerm";

	export default defineComponent({
		props: {
			jobs: {
				required: true,
				type: Array as PropType<Job[]>,
			},

			order: {
				required: true,
				type: String as PropType<OrderTerm>,
			},
		},

		setup(props) {
			const orderedJobs = computed(() => {
				return [...props.jobs].sort((a: Job, b: Job) => {
					return a[props.order] > b[props.order] ? 1 : -1;
				});
			});

			return { orderedJobs };
		},
	});
</script>

<style scoped>
	.job-list {
		max-width: 800px;
		margin: 0 auto;
	}

	ul {
		padding: 0;
		margin: 0;
		list-style: none;
	}

	li {
		padding: 10px 25px 25px 25px;
		margin: 50px auto;
		border: 3.5px solid dodgerblue;
		border-radius: 7px;
		box-shadow: 0 10px 10px rgba(128, 128, 128, 0.25);
		background-color: white;
	}

	.order {
		text-align: right;
		text-transform: capitalize;
		font-weight: bold;
	}

	h2,
	h4 {
		text-transform: capitalize;
	}

	h2 {
		font-family: "Staatliches", cursive;
		letter-spacing: 1.75px;
		font-size: 2.2rem;
		color: rgb(51, 51, 51);
	}

	h4 {
		color: dodgerblue;
		opacity: 0.75;
		font-size: 1.15rem;
	}

	.salary {
		color: rgb(0, 207, 128);
		font-weight: bold;
		font-size: 1.15rem;
	}

	.description {
		font-size: 1.1rem;
		opacity: 0.75;
		width: 95%;
		max-height: 2ch;
		overflow: hidden;
		transition: 0.5s;
		margin: 0 auto;
	}

	li:hover .description {
		max-height: 100px;
	}

	.list-move {
		transition: all 1.5s;
	}

	@media screen and (max-width: 800px) {
		.job-list {
			width: 95%;
		}

		h2 {
			font-size: 1.75rem;
		}
	}
</style>
