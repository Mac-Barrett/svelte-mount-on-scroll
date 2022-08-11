<script lang="ts">
    import { onMount } from "svelte";
    import { fly } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    /** Size Props for the placeholder div, needed in order to properly mount things in succession as opposed to all at once. Default: 100x100 */
    export let placeholderSizeProps: { height?: number, width?: number } = {
        height: 100,
        width: 100
    }

    /** Transition props for when the component mounts. Default: slides in from top */
    export let transitionProps: { x?: number, y?: number, duration?: number, delay?: number } = {
        x: 0,
        y: 0,
        duration: 500,
        delay: 0,
    };

    let mounted = false;
    let div: HTMLElement;
    let innerHeight: number;

    onMount(() => {
        checkToMount();
    });

    function checkToMount() {
        let rect = div?.getBoundingClientRect();
        if(innerHeight > rect?.top) {
            if (mounted === true) return; // Needed so 'mounted' only dispatches once
            dispatch('mounted');
            mounted = true;
        }
    }
</script>

<svelte:window on:scroll={checkToMount} bind:innerHeight></svelte:window>

<div bind:this={div}>
    {#if !mounted}
    <div id="placeholder" style="--height: {placeholderSizeProps.height}px; --width: {placeholderSizeProps.width}px;"></div>
    {:else}
    <div in:fly={{ x: transitionProps.x, y: transitionProps.y, duration: transitionProps.duration, delay: transitionProps.delay }}>
        <slot/>
    </div>
    {/if}
</div>

<style>
    #placeholder {
        height: var(--height);
        width: var(--width);
    }
</style>