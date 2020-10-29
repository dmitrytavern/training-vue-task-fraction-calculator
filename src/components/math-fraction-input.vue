<template>
	<input
			class="math__fraction-input"
			:class="{'is-error': hasError}"
			type="number"
			:style="stylesInput"
			:value="modelValue"
			@input="update($event)"
	>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
	name: "math-fraction",
	props: {
		modelValue: {
			type: Number,
			default: 0,
		},
	},
	data() {
		return {
			hasError: false
		}
	},
	watch: {
		'modelValue'(newVal: number) {
			this.hasError = isNaN(newVal)
		}
	},
	methods: {
		update($event: InputEvent) {
			this.$emit('update:modelValue', +($event.target as HTMLInputElement).value)
		}
	},
	computed: {
		stylesInput(): object {
			const val = this.modelValue.toString().length
			return { width: val+1+'em' }
		},
	}
})
</script>

<style scoped>
.math__fraction-input {
	border: none;
	outline: none;
	background: none;
	height: 30px;
	padding: 5px;
	-moz-appearance: textfield;
	text-align: center;
}

.math__fraction-input.is-error {
	color: #6d1212;
}
</style>