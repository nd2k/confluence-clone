<script lang="ts">
    export let backgroundColor: string = '#52796f';
	export let color: string = 'white';
    export let direction: string = 'row';
    export let width: string = '2rem';
    export let height: string = '2rem';
    export let margin: number = 0;

    $: style = direction === 'row' ? `--background: ${backgroundColor}; 
	--color: ${color}; --flex-direction:${direction}; width: ${width}; height: ${height};`
    : `--background: ${backgroundColor}; 
	--color: ${color}; --flex-direction:${direction}; width: ${width}; height: ${height};`

    $: styleContent = direction === 'row' ? `margin: 0 ${margin}rem;`
    : `margin: ${margin}rem 0;`
</script>

<div class="bar-menu" {style}>
    <div class="content-menu" style={styleContent}>
        <slot />
    </div>
</div>

<style>
    .bar-menu {
        display: flex;
        flex-direction: var(--flex-direction);
        background-color: var(--background);
        color: var(--color);
        border-radius: 5rem;
        position: absolute;
    }
    .content-menu {
        display: flex;
        flex-direction: var(--flex-direction);
        width: 100%;
        height: 100%;
        align-items: flex-start;
        align-items: center;
    }

</style>