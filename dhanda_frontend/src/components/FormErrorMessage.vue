<template>
	<ul v-if="errors.length">
		<li v-for="e in errors">{{ e }}</li>
	</ul>
</template>
<script>
export default {
	props:   {
		errors: {
			type: Array,
			required: true,
		},
	},

	data() {
		return {

		}
	},
}
</script>