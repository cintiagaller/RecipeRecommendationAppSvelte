<script>
    import Card from "./components/Card.svelte";
    import QueryForm from "./components/QueryForm.svelte";
    import RecipeRecommendation from "./components/RecipeRecommendation.svelte";
    import RecipeInfo from "./components/RecipeInfo.svelte";
</script>

<main class="container">
    <Card class="card secondary">
        <h1 class="title-text">Recipe Recommendations</h1>
        <QueryForm />
    </Card>
    <RecipeRecommendation />
</main>

<style>
    .title-text {
        text-align: center;
        padding: 3rem;
        color: #202142;
    }
</style>
