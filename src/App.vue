<template>
	<div id="app">
		<Header :numCorrect="numCorrect" :numTotal="numTotal" />
		<b-container class="bv-example-row" v-if="showSelection">
			<b-col sm="6" offset="3">
				<QuestionBox
					v-if="questions.length"
					:currentQuestion="questions[index]"
					:next="next"
					:increment="increment"
				/>
			</b-col>
		</b-container>
		<b-col sm="8" offset="2" class="OptionsList">
			<b-list-group>
				<b-list-group-item href="#">Default list group item</b-list-group-item>
				<b-list-group-item href="#" variant="primary">Primary list group item</b-list-group-item>
				<b-list-group-item href="#" variant="secondary">Secondary list group item</b-list-group-item>
				<b-list-group-item href="#" variant="success">Success list group item</b-list-group-item>
				<b-list-group-item href="#" variant="danger">Danger list group item</b-list-group-item>
				<b-list-group-item href="#" variant="warning">Warning list group item</b-list-group-item>
				<b-list-group-item href="#" variant="info">Info list group item</b-list-group-item>
				<b-list-group-item href="#" variant="light">Light list group item</b-list-group-item>
				<b-list-group-item href="#" variant="dark">Dark list group item</b-list-group-item>
			</b-list-group>
		</b-col>
	</div>
</template>

<script>
import Header from './components/Header';
import QuestionBox from './components/QuestionBox';

export default {
	name: 'app',
	components: {
		Header,
		QuestionBox
	},
	data() {
		return {
			questions: [],
			index: 0,
			numCorrect: 0,
			numTotal: 0,
			showSelection: false
		};
	},
	methods: {
		next() {
			this.index++;
		},
		increment(isCorrect) {
			if (isCorrect) {
				this.numCorrect++;
			}
			this.numTotal++;
		}
	},
	mounted: function() {
		fetch('https://opentdb.com/api.php?amount=10&category=20&difficulty=easy&type=multiple', {
			method: 'get'
		})
			.then((response) => {
				return response.json();
			})
			.then((jsonData) => {
				this.questions = jsonData.results;
			});
	}
};
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
