<template>
	<div class="result">
		<h2>RESULTS:</h2>
		<table>
			<tr>
				<td>Digits correct</td>
				<td>{{ digits | correctDigits }}</td>
			</tr>
			<tr>
				<td>Time taken</td>
				<td>{{ getDeltaTime() | formatTime }}</td>
			</tr>
			<tr>
				<td>Difficulty</td>
				<td>1 life</td>
			</tr>
			<tr>
				<td>Accuracy</td>
				<td>{{ digits*100/(digits+1) | roundPercent}}</td>
			</tr>
		</table>

		<div class="retrybutton" @click="retry()">Retry</div>
	</div>
</template>

<script>
	export default{
		props: {
			digits: Number,
			retry: Function,
			startTime: Number
		},

		filters: {
			roundPercent(n){
				return Math.round(n*100)/100;
			},

			correctDigits(n){
				return n-(n>1);
			},

			formatTime(n){
				return Math.round((n/1000)*10)/10 + " seconds";
			}
		},

		methods: {
			getDeltaTime(){
				return (new Date().getTime())-this.startTime;
			}
		}
	}
</script>

<style lang="scss">
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

	table > tr > td{
		padding-right:40px;
	}

	.retrybutton{
		border: 1px solid black;
		text-align: center;
		margin: 50px 0px;
		padding: 10px;
		position: absolute;
		bottom: 0;
		left: 20px;
		right: 20px;
	}

	.retrybutton:hover{
		background-color: #eee;
		animation-name: highlight;
  		animation-duration: 0.4s;
	}

	.result{
		text-align: left;
		padding: 20px;
		background-color: #ffffffee;
		position: absolute;
		left: 5%;
		top: 5%;
		right: 5%;
		bottom: 5%;
		border: 1px solid black;
	}
</style>