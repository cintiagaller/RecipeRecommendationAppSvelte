<script>
    import { IngredientList } from "../stores";
    import { fade, scale } from "svelte/transition";
    import Ingredient from "./Ingredient.svelte";
</script>

<div class="filters">
    {#each $IngredientList as ing (ing.id)}
        <div in:scale out:fade={{ duration: 500 }}>
            <Ingredient ingredient={ing} />
        </div>
    {/each}
</div>

<style>
    .filters {
        display: flex;
        justify-content: start;
        flex-wrap: wrap;
        margin: 20px 0;
    }
</style>
