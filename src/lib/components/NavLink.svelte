<script lang="ts">
    import { createEventDispatcher } from 'svelte';

    export let isActive: boolean = false;

    const dispatch = createEventDispatcher();
    const emitHooverEvent = (e: MouseEvent) => {
        dispatch('nav-link-hoover', e.target);        
    }
    const emitUnHooverEvent = (e:MouseEvent) => {
        dispatch('nav-link-unhoover', e.target)
    }
</script>

<li class="list" class:active={isActive} on:mouseenter={emitHooverEvent} on:mouseleave={emitUnHooverEvent}>
    <b></b>
    <b></b>
    <a href="/">
        <span class="icon">
            <slot name="icon" />
        </span>
        <span class="label">
            <slot name="label" />
        </span>
    </a>
</li>

<style>
    li {
        position: relative;
        list-style: none;
        width: 100%;
        border-top-left-radius: 20px;
        border-bottom-left-radius: 20px;
        margin: 0.5rem 0;
    }
    li b:nth-child(1) {
        position: absolute;
        background-color: var(--white-color);
        top: -1rem;
        height: 1rem;
        width: 100%;
        display: none;
    }
    li b:nth-child(1)::before {
        content: '';
        position: absolute;
        background-color: var(--tertiary-color);
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        border-bottom-right-radius: 30px;
    }
    li b:nth-child(2) {
        position: absolute;
        background-color: var(--white-color);
        bottom: -1rem;
        height: 1rem;
        width: 100%;
        display: none;
    }
    li b:nth-child(2)::before {
        content: '';
        position: absolute;
        background-color: var(--tertiary-color);
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        border-top-right-radius: 30px;
    }
    li.active {
        background-color: var(--white-color);
    }
    li.active b:nth-child(1) {
        display: block;
    }
    li.active b:nth-child(2) {
        display: block;
    }
    li.active a {
        color: var(--primary-color);
    }
    li a {
        position: relative;
        display: block;
        width: 100%;
        display: flex;
        text-decoration: none;
        color: var(--white-color);
    }
    li a .icon {
        position: relative;
        display: block;
        min-width: 3rem;
        height: 3rem;
        line-height: 3.8rem;
        text-align: center;
    }
    li a .label {
        position: relative;
        display: block;
        height: 3rem;
        line-height: 3rem;
        padding-left: 1rem;
        white-space: normal;
    }
</style>