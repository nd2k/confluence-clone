<script lang="ts">
    export let hoverColor: string = 'var(--primary-color)'

    $: style = `--hoverColor: ${hoverColor};`

</script>

<div class="menu-element" {style}>
    <slot />
</div>

<style>
    .menu-element {
        display: flex;
        align-items: center;
        cursor: pointer;
        padding: 0.5rem;
    }
    .menu-element:hover {
        color: var(--hoverColor);
        transform: translateY(3px);
    }
</style>