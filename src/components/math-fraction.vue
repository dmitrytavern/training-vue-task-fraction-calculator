<template>

	<div class="math__fraction-container">

		<div class="math__fraction-operator">
			<select class="math__fraction-input select" v-model="fraction.operator">
				<option value="+">+</option>
				<option value="-">-</option>
			</select>
		</div>

		<div class="math__fraction">
			<input class="math__fraction-input" type="number" v-model.number="fraction.numerator">
			<span></span>
			<input class="math__fraction-input" type="number" v-model.number="fraction.denominator">
			<button class="btn btn-remove" @click="remove" v-if="canRemove">-</button>
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
	width: 50px;
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
	width: 30px;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
}

.math__fraction-input.select {
	width: 40px;
}
</style>