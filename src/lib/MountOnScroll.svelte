<!-- ShowOnScroll mounts an element to the screen once it comes into view of the browser window -->
<script lang="ts">
    import { onMount } from "svelte";
    import { fly } from 'svelte/transition'

    /** Size Props for the placeholder div, needed in order to properly mount things in succession as opposed to all at once. Default: 100x100 */
    interface SizeProps {
        height?: number,
        width?: number 
    }
    export let placeholderSizeProps: SizeProps = {
        height: 100,
        width: 100
    }

    /** Transition props for when the component mounts. Default: slides in from top */
    interface TransitionProps {
        x?: number,
        y?: number,
        duration?: number,
        delay?: number
    }
    export let transitionProps: TransitionProps = {
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

<!-- @component
```ts
interface SizeProps {
    height?: number,
    width?: number 
}
// Default Values
export let placeholderSizeProps: SizeProps = {
    height: 100,
    width: 100
}


interface TransitionProps {
    x?: number,
    y?: number,
    duration?: number,
    delay?: number
}
// Default Values
export let transitionProps: TransitionProps = {
    x: 0,
    y: 0,
    duration: 500,
    delay: 0,
};
```
-->

<style>
    #placeholder {
        height: var(--height);
        width: var(--width);
    }
</style>