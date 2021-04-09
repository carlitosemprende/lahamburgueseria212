<script>
	import Router from 'svelte-spa-router';
	import Header from './Header.svelte';
	import ArticleDetail from './components/ArticleDetail.svelte';
</script>
	

<Router routes={{
	'/': Header,
	'/Detail': ArticleDetail
}}/>
