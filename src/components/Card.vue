<template>
	<div class="card">
		<h1>card</h1>
		<p>ID: {{ number }}</p>

		<button @click="changeVersion">Change Version</button>
		<p> versione card {{ version }}</p>


		<Form @submit="onSubmit" class="custom-form">

			<Input name="nome"></Input>
			<Input name="cognome"></Input>

			<button>submit</button>
		</Form>

		<!-- <input v-model="value" placeholder="Type something" name="nome" />
		<span>{{ errorMessage }}</span>


		<button @click="isValid">validate</button> -->

		<!-- <Form @submit="onSubmit">
			<Input />
		</Form> -->



	</div>
</template>

<script setup>
import { Form } from 'vee-validate';
import { useField } from 'vee-validate';
import { ref, computed } from '@vue/reactivity';
import Input from './Input.vue'





// const isValid = ref(false);

const onSubmit = (values) => {

	console.log(values)

}

const props = defineProps(['numero']);

const number = ref(props.numero);
const version = ref('1.0.0')




let versionNumber = 0;
const changeVersion = () => {

	version.value = `1.0.${++versionNumber}`;
}

defineExpose({

	version,
	changeVersion,
	// isValid,
	// onSubmit

})

</script>

<style scoped>
.card {
	padding: 1rem;
	border: 1px solid white;
	border-radius: 8px;
}
</style>