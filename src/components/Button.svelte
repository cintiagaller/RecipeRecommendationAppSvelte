<script>
    let buttonProps = {
        class: [$$restProps.class],
    };
    export let type = "button";
    export let disabled = false;
</script>

<button {type} {disabled} {...buttonProps} on:click>
    <slot />
</button>

<style>
    button {
        color: #fff;
        border: 0;
        border-radius: 8px;
        height: 40px;
        width: 100px;
        cursor: pointer;
    }

    .primary {
        background-color: #202142;
    }

    .secondary {
        background: #d93262;
        width: 100%;
    }

    button:hover {
        transform: scale(0.98);
        opacity: 0.9;
    }

    button:disabled {
        background-color: #cccccc;
        color: #333;
        cursor: auto;
    }

    button:disabled:hover {
        transform: scale(1);
        opacity: 1;
    }
</style>
