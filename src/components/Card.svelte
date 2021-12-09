<script>
    let cardProps = {
        class: [$$restProps.class],
    };
</script>

<div {...cardProps}>
    <slot />
</div>

<style>
    .card {
        border-radius: 15px;
        padding: 40px 50px;
        margin: 20px 0;
        position: relative;
    }

    .primary {
        background-color: #fff;
        color: #333;
    }

    .secondary {
        background-color: #e2c7c8;
        color: #333;
    }

    .light-blue {
        background-color: #e5e5f2;
        color: #333;
    }
    .darker-blue {
        background-color: #bdbee5;
        color: #333;
    }
</style>
