<template>

	<div class="math__fraction-container">

		<div class="math__fraction-operator" v-if="index !== 0">
			<select class="math__fraction-select" v-model="fraction.operator">
				<option value="+">+</option>
				<option value="-">-</option>
			</select>
		</div>

		<div class="math__fraction">
			<MathFractionInput v-model="fraction.numerator" />
			<span></span>
			<MathFractionInput v-model="fraction.denominator" />

			<button class="math__fraction-btn btn btn-remove" @click="remove" v-if="canRemove">
				<svg>
					<use xlink:href="@/assets/trash.svg#ico"></use>
				</svg>
			</button>
		</div>
	</div>

</template>

<script lang="ts">
import { defineComponent } from 'vue'
import MathFractionInput from '@/components/math-fraction-input.vue'

export default defineComponent({
	name: "math-fraction",
	components: {
		MathFractionInput
	},
	props: {
		fraction: Object,
		index: Number,
		canRemove: Boolean,
	},
	methods: {
		remove() {
			this.$emit('remove', this.index)
		},
	},
})
</script>

<style scoped>
.math__fraction {
	display: flex;
	flex-direction: column;
	align-items: center;
}

.math__fraction-container {
	display: flex;
	align-items: center;
	padding: 0 10px;
}

.math__fraction-operator {
	margin-right: 10px;
}

.math__fraction span {
	width: 70%;
	height: 2px;
	background: #000;
	margin: 5px 0;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
	-webkit-appearance: none;
	margin: 0;
}

.math__fraction-select {
	width: 1.6em;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
	background: none;
	appearance: none;
	text-align: center;
	border: none;
	outline: none;
}

.math__fraction-btn {
	padding: 3px;
}

.math__fraction-btn > svg {
	height: 100%;
	fill: #6d1212;
}
</style>