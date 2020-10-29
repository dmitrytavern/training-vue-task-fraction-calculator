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

	</div>

	<div class="math__result">
		Result: <b>{{ math }}</b>
	</div>

	<button class="math__btn-add btn" @click="addFraction">Add fraction</button>
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
					numerator: 0,
					denominator: 0,
					operator: '+',
				},
				{
					numerator: 0,
					denominator: 0,
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
			val = +val.toFixed(2)
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

.math__result {
	margin-top: 15px;
}

.math__btn-add {
	margin-top: 15px;
	border: 1px solid #eee;
	padding: 7px 15px;
	color: #242424;
	transition: all .180s;
}
.math__btn-add:hover {
	background: #eeeeee;
}
</style>