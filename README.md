# Svelte MountOnScroll Component:
### Getting Started:
Installing:
```bash
npm i @mac-barrett/svelte-mount-on-scroll
```

Importing to your page or components:
```ts
import { MountOnScroll } from '@mac-barrett/svelte-mount-on-scroll';
```
### See Also:
[github.com](https://github.com/Mac-Barrett/svelte-mount-on-scroll/)

## About:
Mounts a component to the screen once the component is in view of the browser's viewport.
Useful for making snappy websites, where information or paragraphs are contained inside of the MountOnScroll component.
Uses the built in svelte/transitions fade & fly

### Properties:
Optional properties for customizing how your child components will come into view:

```ts
/** Used to define the config of the transition. If x or y key exists, then the "fly" transition is implicitly chosen. */
export let transitionProps: Partial<{ x: number, y: number, duration: number, delay: number }>= (default: undefined)

/** Will dismount the component when it is no longer on the screen */
export let dismounts: boolean
```

### Events:
- mountStart - Dispatched when the element(s) have started their animation and are mounting to the DOM.
- mountEnd - Dispatched when the element(s) have finished their animation and are mounted to the DOM.
- dismount - Dispatched when the element(s) have dismounted from the DOM.

## Basic use example:
You may choose to fill every field out or you may leave some blank:

```svelte
<MountOnScroll transitionProps={{ duration: 1000 }}>
    <h1>A MountOnScroll that simply fades in.</h1>
</MountOnScroll>

<MountOnScroll transitionProps={{ x: -200, y: 0, duration: 500, delay: 0 }}>
    <h1>A MountOnScroll that flys in from the left.</h1>
</MountOnScroll>

<MountOnScroll
    dismounts={true}
    transitionProps={{ x: 400, y: 0, duration: 4000, delay: 0 }}
    on:mountStart={() => console.log('Hello World!')}
    on:mountEnd={() => console.log('I have finished mounting!')}
    on:dismount={() => console.log('Goodbye, sweet prince...')}
>
    <h1 class="inside">A MountOnScroll with all of its components defined.</h1>
</MountOnScroll>
```