<template>
	<div class="touchbtn" @mouseover="hovering=true" @mouseout="hovering=false" :class="{outline: hovering}">
		{{label}}
	</div>
</template>

<script>
	export default{
		props: {
			label: String,
		},

		data: function(){
			return{
				hovering: false
			}
		}
	}
</script>

<style>
	@keyframes highlight{
		from {
			border: 1px solid #bbb;
			background-color: white;
		}

		to {
			border: 1px solid black;
			background-color: #eee;
		}
	}

	.touchbtn{
		width: 10vw;
		height: 10vw;
		min-width: 100px;
		min-height: 100px;
		border: 1px solid #bbb;
		margin: 5px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 45px;
	}

	.outline{
		border: 1px solid black;
		background-color: #eee;
		animation-name: highlight;
  		animation-duration: 0.4s;
	}
</style>