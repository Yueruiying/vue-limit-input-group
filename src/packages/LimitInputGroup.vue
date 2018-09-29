<template>
    <div>
        <slot/>
    </div>
</template>
<script>
	export default {
		name: 'limit-input-group',
		provide() {
			return {
				inputGroup: this,
				groupMax: this.max,
				groupMin: this.min
			}
		},
		props: {
			max: {
				type: Number,
				default: 10
			},
			min: {
				type: Number,
				default: 0
			}
		},
		data() {
			return {}
		}
	}
</script>