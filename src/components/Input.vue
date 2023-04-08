<template>
	<div>
		<input v-model="value" type="text" />
		<span>{{ errorMessage }}</span>
	</div>
</template>
<script setup>
import { useField } from 'vee-validate';
import { defineProps } from 'vue';
const props = defineProps({
	name: {
		type: String,
		required: true,
	},
});
function isRequired(value) {


	if (props.name === 'nome') {
		if (value && value.trim()) {
			return true;
		}
		return 'Nome è richiesto';
	}


	if (props.name === 'cognome') {
		if (value && value.trim()) {
			return true;
		}
		return 'Cognome è richiesto';
	}

}

// make sure to wrap the name in a function to maintain its reactivity
// this way vee-validate can react to the field name changing
const { errorMessage, value } = useField(() => props.name, isRequired);
</script>