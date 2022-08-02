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

## Properties:
Optional properties for customizing how your component will come into view:

```js
/** Size Props for the placeholder div, needed in order to properly mount things in succession as opposed to all at once. Default: 100x100 */
placeholderSizeProps = {
    height: number,
    width: number
}

/** Transition props for when the component mounts. Default: slides in from top */
transitionProps = {
    x: number,
    y: number,
    duration: number,
    delay: number,
}
```

## Basic use example:
You may also chose to leave the placeholderSizeProps & transitionProps fields empty, doing so will give you default behavior which is equivalent to the example below.

```svelte
<MountOnScroll placeholderSizeProps={{height: 100, width: 100}} transitionProps={{x: 0, y: -100, duration: 500, delay: 0}}>
    <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Aliquam debitis, fugit pariatur sunt, laboriosam rerum nulla corporis tempora magnam nostrum aperiam quo atque sequi voluptate, aut hic omnis a eaque.</p>
</MountOnScroll>
```