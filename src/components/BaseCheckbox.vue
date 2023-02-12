<template>
	<!-- Checkboxes binds to the checked prop, not input, change, etc,
 and triggers change, not input events -->
	<input
		type="checkbox"
		:checked="modelValue"
		@change="$emit('update:modelValue', $event.target.checked)"
		class="field"
	/>
	<label v-if="label">{{ label }}</label>
</template>

<script>
export default {
	props: {
		label: {
			type: String,
			default: '',
		},
		modelValue: {
			type: Boolean,
			default: false,
		},
	},
};
</script>
