<script>
import JeopardyGrid from './routes/JeopardyGrid.svelte'
import QuestionShower from './routes/QuestionShower.svelte'
import AnswerShower from './routes/AnswerShower.svelte'
import MinigameShower from './routes/MinigameShower.svelte'
import NotFound from './routes/NotFound.svelte'
import Router from 'svelte-spa-router'
import { setContext } from 'svelte'

/**
 * 5 by 5 board
 */ 
const routes = {
    // Exact path
    '/': JeopardyGrid,
 
    '/question/:category/:number': QuestionShower,
    '/answer/:category/:number': AnswerShower,
    '/minigame/:number': MinigameShower,
 
    // Catch-all
    // This is optional, but if present it must be the last
    '*': NotFound,
}
let hash = window.location.hash
function routeLoaded() {
	hash = window.location.hash
}
let visited = [[], [], [], [], []].map(arr => [false, false, false, false, false])
let questions = [[], [], [], [], []].map(arr => [false, false, false, false, false])
let answers = [[], [], [], [], []].map(arr => [false, false, false, false, false])
setContext('visited', visited)
setContext('questions', questions)
setContext('answers', answers)
</script>

<main>
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