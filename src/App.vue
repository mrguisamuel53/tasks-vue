<template>
	<div id="app">
		<h1>Tasks</h1>
		<!-- <button @click="outroTeste()">a</button> -->
		<Bar :percentageWidth="logs.length" :difference="counter"/>
		<InputBar @sizeMyTasks="repeatTime = $event" @setMessage="logs.push($event)"/>
		<span class="blocks">
			<span v-for="i in logs.length" :key="i">
				<Task @stoppingCount="option = $event" @removingTask="selectedTask = $event, resetValues()" @sendValue="counter += $event" :taskMessage="logs[i-1]"/>
			</span>
			<p v-if="logs.length <= 0" class="warning-text">You're up to date.</p>
		</span>
	</div>
</template>

<script>
import Bar from '@/components/Bar.vue'
import InputBar from '@/components/InputBar.vue'
import Task from '@/components/Task.vue'

export default {
	components: { Bar, InputBar, Task },
	data() {
		return {
			repeatTime: 0,
			logs: [],
			counter: 0,
			selectedTask: '',
			option: false
		}
	},
	methods: {
		resetValues() {
			let i;
			for(i = 0; i < this.logs.length; i++) {
				if(this.logs[i] == this.selectedTask) {
					this.logs.splice(i,1);
				}
			}
			this.selectedTask = '';
			if(this.counter > 0 && !this.option) this.counter--;
			else this.counter = 0;
			// console.log(this.selectedTask);
		},
	},
}
</script>

<style>
	body {
		font-family: 'Fredoka One', cursive;
		background: linear-gradient(to right, rgb(56, 184, 17), rgb(58, 115, 82));
		color: black;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
		width: 100%;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}

	.blocks {
		display: flex !important;
		flex-direction: row !important;
		flex-wrap: wrap;
		width: 100%;
		justify-content: center;
		align-items: center;
	}

	.warning-text {
		font-size: 2.5rem;
	}
</style>
