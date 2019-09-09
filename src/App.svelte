<script>
	export let name;

	import { onMount } from "svelte";
    
	const API_KEY = "e40d07f00b094602953cc3bf8537477e";
	const URL = `https://newsapi.org/v2/everything?q=comics&sortBy=publishedAt&apiKey=${API_KEY}`;
    let articles = [];

    onMount(async function() {
    	const response = await fetch(URL);
    	const json = await response.json();

		console.log(json);
    	articles = json["articles"];
	});

</script>

<style>

h1 {
	color: purple;
}

.grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
	grid-gap: 20px;
	align-items: stretch;
}

.grid>article {
	border: 1px solid #ccc;
	box-shadow: 2px 2px 6px 0px rgba(0, 0, 0, 0.3);
	font-family: "Comic Sans MS", "Comic Sans", cursive;
}

.grid>article img {
	max-width: 100%;
}

.grid .text {
	padding: 20px;
}

</style>

<h1>
	<img src="https://dailyplanetdc.files.wordpress.com/2018/12/cropped-daily-planet-logo.jpg?w=656&h=146" />
	<p class="about">
			The Daily Planet is where heroes are born and the story continues. We are proud to report on the planet, daily.
	</p>
</h1>

<div class="container">
	<main class="grid">
		{#each articles as article}
			<article>
				<img src="{article.urlToImage}">
				<div class="text">
					<h3>{article.title}</h3>
					<p> {article.description} </p>
					<a href="{article.url}">Read story</a>
				</div>
			</article>
		{/each}
	</main>
</div>

