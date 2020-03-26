<template>
	<div class="Displaybar">
		π = {{pi | overflowManager}}
	</div>
</template>

<script>
	export default{
		props: {
			pi: String
		},

		filters: {
			overflowManager(str){
				const w = document.getElementsByClassName("Displaybar")[0];
				const n = w != undefined ? w.clientWidth / 90 : 5;

				return str.substr(0, n).length < str.length ? "..." + str.substr(str.length-n+1, n) : str;
			}
		}
	}
</script>

<style>
	.Displaybar{
		border: 1px solid black;
		width: 80vw;
		height: 10vh;
		margin-left: 10vw;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 45px;
		overflow: hidden;
	}
</style>