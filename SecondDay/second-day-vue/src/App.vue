<script>
const ArrQuotes = [
	{
		quote:
			"&quot;This is just a Quote1&quot;,fsdfsdgsgfgssdfgsdfghfsh",
		source: 'Edward Elric'
	},
	{
		quote: 'This is just a Quote2',
		source: 'Homer'
	},
	{
		quote: 'This is just a Quote3',
		source: 'Gendo Ikari'
	},
	{
		quote:
			"This is just a Quote4",
		source: ''
	}
]

export default {
	data() {
		return { quotes: ArrQuotes, IsAuthor: '-', SortQuote: [], Name: 'Yehor' }
	},
	computed: {
		FilteredQuotes: function () {
			return this.quotes.filter(element => {
				return Boolean(this.IsAuthor) == Boolean(element.source)
			})
		}
	},
	methods: {
		SortedQuote() {
			this.SortQuote = this.quotes.sort((a, b) =>
				a.source > b.source ? 1 : -1
			)
		},
		GetName() {
			console.log(this.Name)
		}
	}
}
</script>

<template>
	<div id="app">
		<div class="Target">
			<input type="radio" name="Filter" v-model="IsAuthor" value="exist" />
			HaveAutor
			<input type="radio" name="Filter" v-model="IsAuthor" value="" />
			NoAuthor
			<button @click="SortedQuote()">Sort</button>
			<button v-on:click="GetName()" v-on:mouseenter="GetName()" v-on:mousedown="GetName()">
				Three Events
			</button>
		</div>
		<br />
		<div v-for="quote in FilteredQuotes" class="QuotesBlock" :key="quote.quote">
			<h4 v-bind:class="quote.quote.length > 40 ? 'LongQuote' : 'ShortQuote'">
				{{ quote.quote }}
			</h4>
			<h5 class="Autor">{{ quote.source }}</h5>
			<br />
		</div>
		<hr />
		<div v-for="quote in SortQuote" class="SortBlock" :key="quote.quote">
			<h4 v-bind:class="quote.quote.length > 40 ? 'LongQuote' : 'ShortQuote'">
				{{ quote.quote }}
			</h4>
			<h5 class="Autor">{{ quote.source }}</h5>
			<br />
		</div>
	</div>
</template>

<style scoped>
header {
	line-height: 1.5;
}

.logo {
	display: block;
	margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
	header {
		display: flex;
		place-items: center;
		padding-right: calc(var(--section-gap) / 2);
	}

	header .wrapper {
		display: flex;
		place-items: flex-start;
		flex-wrap: wrap;
	}

	#app {
		margin: 0, auto;
		align-items: center;
	}

	.Autor {
		text-align: right;
	}

	.QuotesBlock {
		width: 400px;
		margin-left: auto;
		margin-right: auto;
	}

	.SortBlock {
		width: 400px;
		margin-left: auto;
		margin-right: auto;
	}

	.LongQuote {
		text-decoration: underline;
		color: red;
	}

	.ShortQuote {
		text-transform: capitalize;
		font-weight: lighter;
	}

	.Target {
		width: 400px;
		margin-left: auto;
		margin-right: auto;
	}
}
</style>
