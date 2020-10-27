<template>
	<div class="math">

		<MathFraction
				v-for="(fraction, index) in fractions"
				:fraction="fraction"
				:index="index"
				:key="index"
				:can-remove="fractions.length > 2"

				v-on:remove="removeFraction"
		/>

		<div class="math__symbol">=</div>
		<div class="math__result">{{ math }}</div>

	</div>

	<button class="math__add" @click="addFraction">Add fraction</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import MathFraction from '@/components/math-fraction.vue'

export default defineComponent({
	name: "math",
	components: {
		MathFraction,
	},
	data() {
		return {
			fractions: [
				{
					numerator: 1,
					denominator: 2,
					operator: '+',
				},
				{
					numerator: 1,
					denominator: 2,
					operator: '+',
				},
			]
		}
	},
	computed: {
		math(): number {
			let val = 0
			this.fractions.forEach((fraction) => {
				const numerator = fraction.numerator || 0
				const denominator = fraction.denominator || 0
				const value = numerator / denominator

				if (!isNaN(value) && value !== Infinity) {
					switch (fraction.operator) {
						case '+': val += value; break;
						case '-': val -= value; break;
						default: val += value;
					}
				}
			})
			return val
		}
	},
	methods: {
		addFraction() {
			this.fractions.push({
				numerator: 0,
				denominator: 0,
				operator: '+',
			})
		},

		removeFraction(index: number) {
			this.fractions.splice(index, 1)
		},
	},
})
</script>

<style scoped>
.math {
	display: flex;
	align-items: center;
	justify-content: center;
	margin-top: 30px;
}

.math__symbol,
.math__result {
	font-size: 22px;
	padding: 0 10px;
}

.math__add {
	margin-top: 15px;
}
</style>