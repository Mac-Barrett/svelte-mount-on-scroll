## This Repository:
Contains a basic demo app for the svelte-mount-on-scroll component

to use:

```bash
npm i @mac-barrett/svelte-mount-on-scroll
```

then in your svelte file's script tag:
```ts
import { MountOnScroll } from '@mac-barrett/svelte-mount-on-scroll';
```

## About:
Mounts a component to the screen once the component is in view of the browser's viewport.
Useful for making snappy websites, where information or paragraphs are contained inside of the MountOnScroll component.
Uses the built in svelte/transition fly

#### Properties:
Optional properties for customizing how your child components will come into view:

```ts
/** Size Props for the placeholder div, needed in order to properly mount things in succession as opposed to all at once. Default: 100x100 */
export let placeholderSizeProps: { height?: number, width?: number } = {
    height: 100,
    width: 100
}
/** Transition props for when the component mounts. Default: Does nothing */
export let transitionProps: { x?: number, y?: number, duration?: number, delay?: number } = {
    x: 0,
    y: 0,
    duration: 500,
    delay: 0,
};
```

#### Events:
```ts
dispatch('mounted');
```
Triggered when the component mounts to the screen.  
Use for whatever you'd like or suggest features for arguments to be passed through to make it more useful.

## Basic use example:
You may choose to fill every field out or you may leave some blank:

```svelte
<MountOnScroll transitionProps={{x: 0, y: -100, duration: 500, delay: 0}}>
    <p>
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. 
    </p>
</MountOnScroll>

<MountOnScroll placeholderSizeProps={{height: 200}} transitionProps={{y: -100, duration: 500}}>
    <div>
        Lorem ipsum dolor sit, amet consectetur adipisicing elit.
    </div>
</MountOnScroll>
```