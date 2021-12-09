<script>
    import { IngredientList } from "../stores";
    import Pill from "./Pill.svelte";
    export let ingredient;

    const handleDelete = (ingredientId) => {
        IngredientList.update((currentIngredients) => {
            return currentIngredients.filter((ingredient) => ingredient.id != ingredientId);
        });
    };
</script>

<Pill>
    <button class="close" on:click={() => handleDelete(ingredient.id)}>X</button>
    <p class="text-display">
        {ingredient.text}
    </p>
</Pill>

<style>
    .close {
        position: absolute;
        top: -10px;
        right: -10px;
        width: 26px;
        height: 26px;
        border-radius: 50%;
        background: #9597cc;
        color: #fff;
        border: 1px #eee solid;
        padding: 6px;
        text-align: center;
        font-size: 12px;
        cursor: pointer;
    }
    .text-display {
        padding-right: 20px;
    }
</style>
