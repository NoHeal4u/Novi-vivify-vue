

<template>
	<div>ASD</div>

</template>


<script>
	import Parent from './Parent.vue'

	export default{

		extends: Parent,

		created(){
			console.log('Child')
		}
	}

</script>