<script lang="ts">
    export let isActive: boolean = false;
</script>

<div id="main-page" class:active={isActive}>
    <slot />
</div>

<style>
    #main-page {
        box-sizing: initial;
        background-color: var(--white-color);
        width: 93vw;
        height: 80vh;
        position: fixed;
        left: 5.5rem;
        top: 4rem;
        transition: 0.5s;
    }
    #main-page.active {
        left: 16.8rem;
        width: 80.1vw;
    }
</style>