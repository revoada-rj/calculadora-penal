<template>
	<div class="px-5 py-5">
		<div class="flex flex-col md:flex-row items-center gap-4">
			<img src="/img/logo.png" alt="Discover Nuxt 3" />
			<div class="px-4 mt-4">
				<h1 class="text-5xl font-bold text-blue-custom">Calculadora Penal</h1>
				<small>A calculadora é uma maneira rápida e simples de realizar a somatória de
					todas as imputações penais.</small>
			</div>
		</div>
		<FormCalculadora class="px-4 py-5" />
	</div>
</template>

<script>
	import FormCalculadora from "~/components/calculadora-penal/form.vue";
	export default {
		name: "CalculadoraPenalIndex",
		components: {
			FormCalculadora,
		},
		mounted() { },
	};
</script>