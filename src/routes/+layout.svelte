<script lang="ts">
    import '../styles/main.css';
    import { fade } from 'svelte/transition';
    import Button from '$lib/components/Button.svelte';
    import Menu from '@svicons/boxicons-regular/menu.svelte';
    import Sidenav from '$lib/Sidenav.svelte';
    import MainContent from '$lib/MainContent.svelte';

    let isMainMenuOpened: boolean = false;
    let isMainContentOpened: boolean = false;

    const toggleMenu = () => {
        isMainMenuOpened = !isMainMenuOpened;
    }

    const openMenu = () => {
        isMainMenuOpened = true;
    }

    const closeMenu = () => {
        isMainMenuOpened = false;
    }

    const activeMainContent = () => {       
        isMainContentOpened = !isMainContentOpened;
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
            <div class="sidenav" transition:fade={{ duration: 500 }}>
                <Sidenav on:active-main-content={activeMainContent}/>
            </div> 
        {/if}
        
        <div id="main-content" on:mouseenter={closeMenu}>
            <MainContent isActive={isMainContentOpened}>
                <slot />
            </MainContent>
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
        top: 0.8rem;
        left: 1.3rem;
        position: fixed;
        z-index: 100;
    }
</style>