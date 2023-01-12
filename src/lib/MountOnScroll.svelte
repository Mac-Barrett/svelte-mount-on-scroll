<script>
    import { onMount } from "svelte";
    import { fade, fly } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    
    /** @type {Partial<{ x: number, y: number, duration: number, delay: number }>=} */
    export var transitionProps = undefined;
    
    /** @type {boolean} */
    export var dismounts = false;

    const dispatch = createEventDispatcher();

    /** @type {boolean} */
    let mounted = false;
    /** @type {HTMLDivElement}*/
    let div;
    /** @type {number} */
    let innerHeight;

    // check for mounting right away in case the element is already in view.
    onMount(() => {
        checkToMount();
    });

    /**
     * Checks to see if the component can be mounted based on the Client's scroll position
     */
    function checkToMount() {
        // Prevent this function from calling if the slotted element is already mounted. If "dismount" is specified, then this is ignored.
        if (mounted && !dismounts) return; 
        let rect = div?.getBoundingClientRect();
        // Specifying this allows unmounting to only occur when the client's scroll position is outside an offset of the component's height.
        const mountingHeight = innerHeight + (rect?.height * (mounted ? 1 : 0));
        const inView = (mountingHeight > rect?.top) && (rect?.top > (mountingHeight * -1));
        if(mounted && !inView) {
            dispatch('dismount');
        }
        mounted = inView;
    }

    // Build the transition configuration for "in:"
    /** @type {((node: Element) => import("svelte/transition").TransitionConfig)?} */
    $: _transition = (transitionProps != undefined && ("x" in transitionProps || "y" in transitionProps))
        ? (node) => fly(node, transitionProps) : transitionProps != undefined
        ? (node) => fade(node, transitionProps) : null;
</script>

<svelte:window on:scroll={checkToMount} bind:innerHeight></svelte:window>

<div bind:this={div}>
    {#if !mounted}
        <div id="placeholder">
            <slot/>
        </div>
    {:else}
        {#if _transition != null}
            <div in:_transition
                on:introstart={() => dispatch('mountStart')}
                on:introend={() => dispatch('mountEnd')}
            >
                <slot/>
            </div>
        {:else}
            <div>
                <slot/>
            </div>
        {/if}
    {/if}
</div>

<style>
    #placeholder {
        visibility: hidden;
        height: 100%;
        width: 100%;
    }
</style>

<!-- @component Allows for one or more elements to have reactive transitions based on the user's scroll position  
    @Property transitionProps: Partial<{ x: number, y: number, duration: number, delay: number }>= (default: undefined)  
        - Used to define the config of the transition. If x or y key exists, then the "fly" transition is implicitly chosen.  
    @Property dismounts: boolean (default: false)  
        - If specified, then the nested element(s) will dismount from the page when the user is outside of the 2x element's height bounds (not to be confused with the CustomEvent, "dismount")  
    @Dispatches mountStart - Dispatched when the element(s) have started their animation and are mounting to the DOM.
    @Dispatches mountEnd - Dispatched when the element(s) have finished their animation and are mounted to the DOM.
    @Dispatches dismount - Dispatched when the element(s) have dismounted from the DOM.
    @Usage
    ```
    <script>
        function handleMountStart() {
            console.log("element is mounting!");
        }
        function handleMountEnd() {
            console.log("element has mounted!");
        }
        function handleDismount() {
            console.log("element has demounted!");
        }
    </script>
    # fly transition on mount
    <MountOnScroll transitionProps={{x: 100, duration: 1000}}
        on:mountStart={handleMountStart}
        on:mountEnd={handleMountEnd}
        on:dismount={handleDismount}>
        <h5>Hello world!</h5>
    </MountOnScroll>
    # fade transition on mount and unmount the component when it goes out of view.
    <MountOnScroll dismounts transitionProps={{duration: 1000}}>
        <h5>Hello world!</h5>
    </Mount>
    ```
-->