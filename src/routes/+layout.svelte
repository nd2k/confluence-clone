<script lang="ts">
    import '../styles/main.css';
    import { fade } from 'svelte/transition';
    import Button from '$lib/components/Button.svelte';
    import Menu from '@svicons/boxicons-regular/menu.svelte';
    import User from '@svicons/boxicons-regular/user.svelte';
    import Sidenav from '$lib/Sidenav.svelte';
    import MainContent from '$lib/MainContent.svelte';
    import MainMenu from '$lib/MainMenu.svelte';

    let isSidebarOpened: boolean = false;
    let isMainMenuOpened: boolean = false;
    let isMainContentOpened: boolean = false;

    const toggleSidebarMenu = () => {
        isSidebarOpened = !isSidebarOpened;
    }

    const toggleMainMenu = () => {
        isMainMenuOpened = !isMainMenuOpened;
    }

    const openSidebarMenu = () => {
        isSidebarOpened = true;
    }

    const openMainMenu = () => {
        isMainMenuOpened = true;
    }

    const closeMenus = () => {
        isSidebarOpened = false;
        isMainMenuOpened = false;
    }

    const activeMainContent = () => {       
        isMainContentOpened = !isMainContentOpened;
    }
</script>

<div id="main-layout">
    <div id="second-layout">
        <div id="main-btn" on:mouseenter={openSidebarMenu}>
            <Button 
            eventName='main-menu-event' 
            outline={true}
            height={2.5}
            width={2.5}
            rounded={50}
            backgroundColor='var(--white-color)'
            color='var(--primary-color)'
            active={isSidebarOpened}
            on:main-menu-event={toggleSidebarMenu}
            >
                <Menu width="2rem"/>
            </Button>
        </div>

        <div id="user-btn" on:mouseenter={openMainMenu}>
            <Button 
            eventName='user-menu-event' 
            outline={true}
            height={2.5}
            width={2.5}
            rounded={50}
            backgroundColor='var(--white-color)'
            color='var(--primary-color)'
            on:user-menu-event={toggleMainMenu}
            >
                <User width="2rem"/>
            </Button>
        </div>

        {#if isMainMenuOpened}
            <div class="main-menu" transition:fade={{ duration: 500 }}>
                <MainMenu isActive={isMainMenuOpened}/>
            </div>
        {/if}

        {#if isSidebarOpened}
            <div class="sidenav" transition:fade={{ duration: 500 }}>
                <Sidenav on:active-main-content={activeMainContent}/>
            </div> 
        {/if}
        
        <div id="main-content" on:mouseenter={closeMenus}>
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
    #user-btn {
        top: 0.8rem;
        right: 1.3rem;
        position: fixed;
        z-index: 100;
    }
</style>