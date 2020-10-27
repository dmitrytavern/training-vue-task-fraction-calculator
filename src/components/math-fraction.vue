<template>

	<div class="math__fraction-container">

		<div class="math__fraction-operator" v-if="index !== 0">
			<select class="math__fraction-select" v-model="fraction.operator">
				<option value="+">+</option>
				<option value="-">-</option>
			</select>
		</div>

		<div class="math__fraction">
			<input class="math__fraction-input" type="number" :style="stylesNumeratorInputSize" v-model.number="fraction.numerator">
			<span></span>
			<input class="math__fraction-input" type="number" :style="stylesDenominatorInputSize" v-model.number="fraction.denominator">

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

export default defineComponent({
	name: "math-fraction",
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
	computed: {
		stylesNumeratorInputSize(): object {
			const val = this.fraction.numerator.toString().length
			return {
				width: val+1+'em'
			}
		},

		stylesDenominatorInputSize(): object {
			const val = this.fraction.denominator.toString().length
			return {
				width: val+1+'em'
			}
		}
	}
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

.math__fraction-input {
	border: none;
	outline: none;
	background: none;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
	text-align: center;
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