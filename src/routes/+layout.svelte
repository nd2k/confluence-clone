<script lang="ts">
    import '../styles/main.css';
    import Button from '$lib/components/Button.svelte';
    import Menu from '@svicons/boxicons-regular/menu.svelte';
    import Sidenav from '$lib/Sidenav.svelte';

    let isMainMenuOpened: boolean = false;

    const toggleMenu = () => {
        isMainMenuOpened = !isMainMenuOpened;
    }

    const openMenu = () => {
        isMainMenuOpened = true;
    }

    const closeMenu = () => {
        isMainMenuOpened = false;
    }
</script>

<div id="main-layout">
    <div id="second-layout">
        <div id="main-btn" on:mouseenter={openMenu}>
            <Button 
            eventName='main-menu-event' 
            outline={true}
            height={2.5}
            width={2.5}
            rounded={50}
            backgroundColor='var(--white-color)'
            color='var(--primary-color)'
            active={isMainMenuOpened}
            on:main-menu-event={toggleMenu}
            >
                <Menu width="2rem"/>
            </Button>
        </div>

        {#if isMainMenuOpened}
            <div class="sidenav">
                <Sidenav />
            </div> 
        {/if}
        
        <div id="main-content" on:mouseenter={closeMenu}>
            <slot />
        </div>
    </div>
</div>

<style>
    #main-layout {
        background-color: var(--background-color);
        min-width: 100vw;
        min-height: 100vh;
    }
    #second-layout {
        padding: 0.5rem;
    }
    #main-btn {
        padding-top: 0.5rem;
        padding-left: 0.8rem;
        position: absolute;
        z-index: 100;
    }
</style>