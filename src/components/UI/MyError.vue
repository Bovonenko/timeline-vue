<template>
    <div class="error">
		<img src="../../assets/error.gif" alt="Error"/>
		<h5>Something went wrong</h5>
	</div>
</template>

<script>
    export default {
        name: 'my-error'
    }
</script>

<style lang="scss">
.error {
	margin-top: 25px;
	text-align: center;
	img {
		display: block;
		width: 250px; 
		height: 250px; 
		object-fit: contain;
		margin: 0 auto;
	}
    h5 {
        margin-top: 15px;
    }
}
</style>