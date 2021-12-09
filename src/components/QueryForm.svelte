<script>
    import { v4 as uuidv4 } from "uuid";
    import { IngredientList, RecipeResultList } from "../stores";
    import Card from "./Card.svelte";
    import Button from "./Button.svelte";
    import QueryIngredientFilter from "./QueryIngredientFilter.svelte";

    const api = API_KEY;

    let text = "";
    let btnDisabled = true;
    let message;
    const minLength = 3;
    const maxLength = 15;
    let valid = false;
    const alphabeticChars = /^[a-zA-Z ]+$/;

    const handleInput = () => {
        let textLength = text.trim().length;
        let isAlpha = text.trim().match(alphabeticChars) !== null;

        valid = textLength < minLength ? false : textLength > maxLength ? false : isAlpha;

        if (!valid) {
            message = `Ingredient's name must be between ${minLength} and ${maxLength} characters and should only include letter of the alphabet or space.`;
            btnDisabled = true;
        } else {
            message = null;
            btnDisabled = false;
        }
    };

    const handleSubmit = () => {
        if (text.trim().length >= minLength) {
            const newIngredient = {
                id: uuidv4(),
                text,
            };
            IngredientList.update((currentIngredients) => {
                return [newIngredient, ...currentIngredients];
            });
            text = "";
            message = "";
        }
    };

    let ingredients = [];
    let url = "https://api.spoonacular.com/recipes/findByIngredients?ingredients=";

    IngredientList.subscribe((list) => {
        ingredients = list;
    });

    let recipes = [];
    RecipeResultList.subscribe((list) => {
        recipes = list;
    });

    const handleSearch = () => {
        if (ingredients.length > 0) {
            url = url.concat(ingredients[0].text);
            for (let i = 1; i < ingredients.length; i++) {
                url = url.concat(",+", ingredients[i].text);
            }
            url = url.concat(`&number=3&ranking=2&apiKey=${api}`);

            fetchRecommendation().then((data) => {
                RecipeResultList.set(data);
            });
        }
        text = "";
        message = "";
        url = "https://api.spoonacular.com/recipes/findByIngredients?ingredients=";
    };

    const fetchRecommendation = async () => {
        const response = await fetch(url);
        return await response.json();
    };
</script>

<Card class="card primary">
    <header>
        <h2>What's in your fridge?</h2>
    </header>
    <form on:submit|preventDefault={handleSubmit}>
        <div class="input-group">
            <input type="text" on:keyup={handleInput} bind:value={text} placeholder="Add an ingredient" />
            <Button disabled={btnDisabled} class="primary" type="submit">Add</Button>
        </div>
        {#if message}
            <div class="message">
                {message}
            </div>
        {/if}
    </form>
    <QueryIngredientFilter />

    <Button class="secondary" on:click={handleSearch}>Search</Button>
</Card>

<style>
    header {
        max-width: 400px;
        margin: auto;
    }

    header h2 {
        font-size: 22px;
        font-weight: 600;
        text-align: center;
    }
    form {
        margin-bottom: 40px;
    }
    .input-group {
        display: flex;
        flex-direction: row;
        border: 1px solid #ccc;
        padding: 8px 10px;
        border-radius: 8px;
        margin-top: 15px;
    }
    input {
        flex-grow: 2;
        border: none;
        font-size: 16px;
    }
    input:focus {
        outline: none;
    }
    .message {
        padding-top: 10px;
        text-align: center;
        color: rebeccapurple;
        font-weight: bold;
    }
</style>
