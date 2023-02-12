<template>
	<!-- Note that v-bind:is is a handy tool to, in this case, set the type of element -->
	<component
		v-for="option in options"
		:key="option.value"
		:is="vertical ? 'div' : 'span'"
		:class="{
			horizontal: !vertical,
		}"
	>
		<BaseRadio
			:label="option.label"
			:value="option.value"
			:modelValue="modelValue"
			:name="name"
			@update:modelValue="$emit('update:modelValue', $event)"
		/>
	</component>
</template>

<script>
export default {
	props: {
		options: {
			type: Array,
			required: true,
		},
		name: {
			type: String,
			required: true,
		},
		modelValue: {
			type: [String, Number],
			required: true,
		},
		// Common practice is to set props that toggle on and off (aka flags) to false
		// so that we can set them to on with a very clear syntax = ie, vertical instead of vertical="true"
		vertical: {
			type: Boolean,
			default: false,
		},
	},
};
</script>

<style scoped>
.horizontal {
	margin-right: 20px;
}
</style>
