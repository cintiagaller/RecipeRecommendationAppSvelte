<script>
    import { FullRecipes } from "../stores";
    import Card from "./Card.svelte";
    import Button from "./Button.svelte";

    let allRecipeResults = [];
    FullRecipes.subscribe((list) => {
        allRecipeResults = [...list];
    });
</script>

{#if $FullRecipes.length > 0}
    {#each allRecipeResults as recipe}
        <Card class="card light-blue">
            <h3 class="recipe-title">{recipe.title}</h3>
            <!-- svelte-ignore a11y-img-redundant-alt -->
            <img src={recipe.image} alt="Photo of {recipe.title}" class="recipe-img" /><br />
            <Card class="card darker-blue">
                <h4>Ingredients</h4>
                <ul>
                    {#each recipe.extendedIngredients as ingredient}
                        <li>{ingredient.original}</li>
                    {/each}
                </ul>
            </Card>

            <Card class="card primary">
                <h4>Instructions</h4>
                <p>
                    {@html recipe.instructions}
                </p>
            </Card>

            <div class="right-aligned">
                <Button class="primary">
                    <a href={recipe.sourceUrl} target="_blank">See original</a>
                </Button>
            </div>
        </Card>
    {/each}
{/if}

<style>
    .recipe-title {
        padding: 20px 10px;
    }

    .recipe-img {
        width: 98%;
        display: block;
        margin: 0 auto;
        border-radius: 15px;
    }

    .right-aligned {
        display: flex;
        justify-content: flex-end;
    }

    a {
        text-decoration: none;
        color: #fff;
    }
</style>
