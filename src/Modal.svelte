<script>
    // once - makes sure the event can only fire once (removes handler)
    // preventDefault - prevent the default action (run e.preventDefault)
    // self - only fires the event if the clicked element is the target
    export let showModal = true;
    export let isPromo = false;

</script>
{#if showModal}
<div class="backdrop" class:promo={isPromo} on:click|self>
    <div class="modal">
        <slot></slot>
    </div>
</div>
{/if}

<style>
    .backdrop{
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        background: rgba(0, 0, 0, 0.8);

    }
    .modal{
        padding: 10px;
        border-radius: 10px;
        max-width: 400px;
        margin: 10% auto;
        text-align: center;
        background: white;
    }
    .promo .modal{
        background: crimson;
        color: white;
    }
</style>