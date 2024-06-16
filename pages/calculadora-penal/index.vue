<template>
  <div class="px-4 mt-4">
		<h1 class="text-4xl font-bold">Calculadora Penal</h1>
		<small>A calculadora é uma maneira rápida e simples de realizar a somatória de todas as imputações penais.</small>
	</div>
	<FormCalculadora class="px-4 py-5"/>
</template>

<script>
import FormCalculadora from '~/components/calculadora-penal/form.vue';
export default {
  name: "CalculadoraPenalIndex",
	components: {
		FormCalculadora,
	},
  mounted() {},
};
</script>
