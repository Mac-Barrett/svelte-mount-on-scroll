<script>
    import { MountOnScroll } from '$lib';
</script>

<h1 class="desc">Svelte Mount on Scroll component example</h1>
<p>
    Each black box below contains a normal h1 tag, while each box that is colored contains an h1 tag wrapped with the MountOnScroll component
</p>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<MountOnScroll transitionProps={{ x: -200, y: 0, duration: 500, delay: 0 }}>
    <h1 class="inside">Inside of a  MountOnScroll tag. Mounts as soon as the page is loaded.</h1>
</MountOnScroll>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<MountOnScroll>
    <h1 class="inside">A MountOnScroll with 0 config setup</h1>
</MountOnScroll>
<MountOnScroll
    dismounts={true}
    transitionProps={{ x: 400, y: 0, duration: 4000, delay: 0 }}
    on:mountStart={() => console.log('Hello World!')}
    on:mountEnd={() => console.log('I have finished mounting!')}
    on:dismount={() => console.log('Goodbye, sweet prince...')}
>
    <h1 class="inside">Check the console! This component has some events rigged up!</h1>
</MountOnScroll>
<h1>Normal</h1>
<h1>Normal</h1>
<MountOnScroll transitionProps={{ duration: 1000 }}>
    <h1 class="inside">A MountOnScroll that simply fades in.</h1>
</MountOnScroll>
<h1>Normal</h1>
<h1>Normal</h1>


<style>
    h1.desc, p {
        border: none;
    }
    h1 {
        border: 2px solid black;
        border-radius: 5px;
        margin: 3px;
        padding: 12px;
    }
    h1.inside {
        border: 2px solid green;
        background-color: lightgreen;
    }
</style>