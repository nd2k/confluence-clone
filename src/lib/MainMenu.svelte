<script lang="ts">
    import Cog from '@svicons/boxicons-regular/cog.svelte';
    import Login from '@svicons/boxicons-regular/log-in.svelte';
    import Logout from '@svicons/boxicons-regular/log-out.svelte';

    export let isActive: boolean = false;
</script>

<div class="navigation" class:active={isActive}>
    <ul>
        <div class="nav-link">
            <Login width="1.5rem"/>
            <span class="label">Login</span>
        </div>
        <div class="nav-link">
            <Logout width="1.5rem"/>
            <span class="label">Logout</span>
        </div>
        <div class="nav-link">
            <Cog width="1.5rem"/>
            <span class="label">Settings</span>
        </div>
    </ul>
</div>

<style>
    .navigation {
        position: fixed;
        background-color: var(--tertiary-color);
        border-radius: 0.5rem;
        top: 0.5rem;
        right: 0.5rem;
        box-sizing: initial;
        transition: 0.5s;
        z-index: 98;
        height: 7.5vh;
    }
    .navigation.active {
        width: 50vw;
    }
    ul {
        display: flex;
        flex-direction: row;
        align-items: center;
        width: 100%;
        height: 100%;
        color: var(--white-color);
        padding: 0;
        margin: 0;
        width: 50%;
    }
    .nav-link {
        display: flex;
        justify-content: center;
        align-items: center;
        min-width: 8rem;
        height: 100%;
    }
    .nav-link:hover {
        color: var(--primary-color);
        background-color: var(--white-color);
        cursor: pointer;
        width: 250%;
        transition: 0.5s;
    }
    .nav-link:hover:nth-child(1) {
        border-top-left-radius: 0.5rem;
        border-bottom-left-radius: 0.5rem;
    }
    .label {
        margin-left: 0.5rem;
        display: none;
    }
    .nav-link:hover>.label {
        display: block;
    }
</style>