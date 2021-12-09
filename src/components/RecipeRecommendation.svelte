<script>
    import Card from "./Card.svelte";
    import RecipeInfo from "./RecipeInfo.svelte";
    import { RecipeResultList, FullRecipes } from "../stores";
    import { fly } from "svelte/transition";

    let recipesBasic = [];
    let recipesUrl = "";
    let recipesFull = [];
    const api = API_KEY;

    const fetchRecipes = async () => {
        const response = await fetch(recipesUrl);
        return await response.json();
    };

    RecipeResultList.subscribe((list) => {
        recipesBasic = list;
        recipesUrl = getNewURL();

        if (recipesBasic.length > 0) {
            fetchRecipes().then((data) => {
                FullRecipes.set(data);
            });
        }
    });

    function getNewURL() {
        let ids = "";
        let url = "https://api.spoonacular.com/recipes/informationBulk?ids=";
        if (recipesBasic.length > 0) {
            ids = recipesBasic[0].id.toString();
            for (let i = 1; i < recipesBasic.length; i++) {
                ids += ",";
                ids += recipesBasic[i].id.toString();
            }

            url = url.concat(`${ids}&includeNutrition=false&apiKey=${api}`);
        }

        return url;
    }

    FullRecipes.subscribe((list) => {
        recipesFull = list;
    });
</script>

{#if recipesFull.length > 0}
    <div transition:fly={{ y: 200, duration: 1000 }}>
        <RecipeInfo />
    </div>
{/if}
