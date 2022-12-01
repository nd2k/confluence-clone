<!-- <script lang="ts">
    import Barmenu from '$lib/components/Barmenu.svelte';
    import Plus from '@svicons/boxicons-regular/plus-circle.svelte';
    import IconMenu from './components/IconMenu.svelte';
    import { fly } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
  import ElementMenu from './components/ElementMenu.svelte';

    export let isMainMenuOpened: boolean = false;
</script>

<div id="sidenav">
    {#if isMainMenuOpened}
        <div class="horizontal-bar-menu" transition:fly="{{ duration: 200, x: -1000, opacity: 0.5, easing: quintOut}}">
            <Barmenu 
                backgroundColor='var(--tertiary-color)' 
                color='var(--white-color)'
                direction='row'
                width='90%'
                height=3.2rem 
                margin={5}>
                    <IconMenu>
                        New project
                    </IconMenu>
                    <IconMenu>
                        Settings
                    </IconMenu>       
            </Barmenu>
        </div>
    {/if}
    {#if isMainMenuOpened}
        <div class="vertical-bar-menu" transition:fly="{{ duration: 200, y: -1000, opacity: 0.5, easing: quintOut}}">
            <Barmenu 
                backgroundColor='var(--tertiary-color)' 
                color='var(--white-color)' 
                direction='column'
                width='3.2rem'
                height='80vh'
                margin={5} >
                    <ElementMenu>
                        <IconMenu slot='icon'>
                            <Plus width="1.5rem"/>
                        </IconMenu>
                    </ElementMenu>
            </Barmenu>
        </div>
    {/if}
</div>

<style>

</style> -->
<script lang="ts">
    import Plus from '@svicons/boxicons-regular/plus-circle.svelte';
    import { onMount } from 'svelte';
    import NavLink from "./components/NavLink.svelte";

    let sidenav: HTMLElement;
    let navLinks: NodeListOf<HTMLElement>;
    let active: boolean = false;

    onMount(() => {
        navLinks = sidenav.querySelectorAll('.list');
    })

    const setNavLinkActiveState = (e:CustomEvent) => {
        let navLink: HTMLElement = e.detail;
        navLink.classList.add('active');    
        sidenav.classList.add('active');   
    }

    const removeNavLinkActiveState = (e:CustomEvent) => {
        navLinks.forEach(navLink => {
            if (navLink != e.detail) {
                navLink.classList.remove('active');
            }
        })
    }

    const removeNavigationActiveState = (e:CustomEvent) => {
        sidenav.classList.remove('active');
    }
</script>

<div class="navigation" bind:this={sidenav} class:active>
    <ul>
        <NavLink 
            on:nav-link-hoover={(e) => {
                setNavLinkActiveState(e)
                removeNavLinkActiveState(e)
            }}
            on:nav-link-unhoover={(e) => removeNavigationActiveState(e)}>
            <Plus width="1.5rem" slot="icon"/>
            <span slot="label">First</span>
        </NavLink>
        <NavLink 
            on:nav-link-hoover={(e) => {
                setNavLinkActiveState(e)
                removeNavLinkActiveState(e)
            }}
            on:nav-link-unhoover={(e) => removeNavigationActiveState(e)}>
            <Plus width="1.5rem" slot="icon"/>
            <span slot="label">Second</span>
        </NavLink>
    </ul>
</div>

<style>
    .navigation {
        position: fixed;
        width: 3.7rem;
        background-color: var(--tertiary-color);
        border-radius: 0.5rem;
        top: 0.5rem;
        bottom: 1rem;
        left: 0.6rem;
        box-sizing: initial;
        border-left: 5px solid var(--tertiary-color);
        transition: 0.5s;
        overflow-x: hidden;
        z-index: 98;
    }
    .navigation.active {
        width: 15rem;
    }
    .navigation ul {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        padding-top: 3rem;
        padding-left: 0.1rem;
    }
</style>