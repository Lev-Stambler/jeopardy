<script>
import JeopardyGrid from './routes/JeopardyGrid.svelte'
import QuestionShower from './routes/QuestionShower.svelte'
import AnswerShower from './routes/AnswerShower.svelte'
import MinigameShower from './routes/MinigameShower.svelte'
import NotFound from './routes/NotFound.svelte'
import TitlePage from './routes/TitlePage.svelte'
import Router from 'svelte-spa-router'
import { setContext } from 'svelte'

/**
 * 5 by 5 board
 */ 
let routes = {}
setContext('visited', [])
setContext('questions', [])
setContext('answers', [])
let hash = window.location.hash
function routeLoaded() {
	hash = window.location.hash
}
const setStoreProm = setStores()
let answers
let questions
let visited
let categories
async function setStores() {
	const ret = await fetch('http://localhost:8080', {
		method: 'GET', // *GET, POST, PUT, DELETE, etc.
		mode: 'cors', // no-cors, *cors, same-origin
		cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
	})
	const body = await ret.json()
	visited = [[], [], [], [], []].map(arr => [false, false, false, false, false])
	let categoriesNonred = body.questions.map(q => q.category_name)
	categories = categoriesNonred.filter((cat, i) => categoriesNonred.indexOf(cat) === i)
	console.log("AAAA", categories, categoriesNonred)
	let qaFlat = body.questions //.map(question => {return { question_text: question.question_text, answer: question.answer }}) //[[], [], [], [], []].map(arr => [false, false, false, false, false])
	questions = []
	answers = []
	questions.push([], [], [], [], [])
	questions.map(arr => [false, false, false, false, false])
	answers.push([], [], [], [], [])
	answers.map(arr => [false, false, false, false, false])
	for (var i = 0; i < qaFlat.length; i++) {
		const r = categories.indexOf(qaFlat[i].category_name)
		const x = parseInt(qaFlat[i].point_value) / 100 - 1
		questions[r][x] = qaFlat[i].question_text.split("\n").join("<div class='small-space'></div>")
		answers[r][x] = qaFlat[i].answer.replace("\n", "<br />")
		if (questions[r][x].indexOf("a.") !== -1 && questions[r][x].indexOf("b.") !== -1) {
			questions[r][x] = questions[r][x] + `
				<style>
					.statement {
						font-size: 30px;
					}
				</style>
			`
		}
		questions[r][x] = questions[r][x].split("?t").join("'t")
		questions[r][x] = questions[r][x].split("?s").join("'s")
		answers[r][x] = answers[r][x].split("?t").join("'t")
		answers[r][x] = answers[r][x].split("?s").join("'s")
		if (answers[r][x].indexOf(`https://en.wikipedia.org/wiki/List_of_Olympic_medalists_in_figure_skating`) !== -1)
			answers[r][x] = "Consult Hosts"
	}
	routes = {
		// Exact path
		'/': JeopardyGrid,
		'/title': TitlePage,
		'/question/:category/:number': QuestionShower,
		'/answer/:category/:number': AnswerShower,
		'/minigame/:number': MinigameShower,
		
		// Catch-all
		// This is optional, but if present it must be the last
		'*': NotFound,
	}
}
function init() {
	setContext('visited', visited)
	setContext('questions', questions)
	setContext('answers', answers)
	setContext('categories', categories)
	return ""
}
</script>

<main>
{#await setStoreProm}
loading{:then value}
{init()}
	<!-- promise was fulfilled -->
	<div class="page-container">
		{#if hash.length > 2}
		<div class="home icon-container">
			<a href="#/">
				<img src="https://image.flaticon.com/icons/png/512/25/25694.png" alt="">
			</a>
		</div>
		{/if}
		<Router {routes} on:routeLoaded={routeLoaded}/>
	</div>
{:catch error}
{error}
	<!-- promise was rejected -->
{/await}
</main>

<style>
	main {
		margin: 0 auto;
		height: 100%;
		padding: 0;
		color: rgb(211, 211, 211);
	}

	.home {
		position: absolute;
		top: 20px;
		left: 20px;
		filter: invert(70%);
		z-index: 100000;
	}

	.icon-container {
		height: 30px;
		width: 30px;
	}

	.icon-container img {
		width: 100%;
		height: 100%;
	}

	.page-container {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: row;
		margin: 0;
		align-items: center;
		justify-content: center;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>