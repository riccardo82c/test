<template>
	<div class="greetings">
		<h1>store count{{ counter.count }} </h1>
		<h1>store doublecount {{ counter.doubleCount }}</h1>

		<button class="button" @click="counter.increment">Increment in store</button>
		<h1 class="green">{{ msg }}</h1>

		<ul>
			<Card v-for="item in list" ref="itemRefs" :numero="item.id" :text="item.text">
				{{ item }}
			</Card>
		</ul>

		<h2>Current selected version: {{ version }}</h2>
		<div>
			<h3>Select card to add version</h3>

			<select v-model="cardSelected">
				<option :value="l.id" v-for="l in list">
					{{ l.text }}
				</option>
			</select>

			<button @click="changeVersionInParent">changeVersionInParent</button>
		</div>
		<div>

			<h3>validate all forms</h3>
			<button @click="validateAllForm">validate all</button>
		</div>


	</div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { useCounterStore } from "../stores/counter";

import Card from './Card.vue';

const counter = useCounterStore();
const cardSelected = ref(1);

const version = computed(() => itemRefs.value[cardSelected.value - 1]?.version)
const changeVersionInParent = () => itemRefs.value[cardSelected.value - 1]?.changeVersion()


const list = ref([
	{
		id: 1,
		text: 'one'

	},
	{
		id: 2,
		text: 'two'

	},
	{
		id: 3,
		text: 'three'

	}
])

const itemRefs = ref([])

// const validateAllForm = () => console.log(itemRefs.value[0]?.isValid);


onMounted(() => {
	console.log(itemRefs.value[1]?.version);

})


defineProps({
	msg: {
		type: String,
		required: true,
	},
});
</script>

<style scoped>
ul {
	padding: 0;
}

h1 {
	font-weight: 500;
	font-size: 2.6rem;
	top: -10px;
}

h3 {
	font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
	text-align: center;
}

@media (min-width: 1024px) {

	.greetings h1,
	.greetings h3 {
		text-align: left;
	}
}
</style>
