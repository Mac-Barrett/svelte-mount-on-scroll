<script>
    import { MountOnScroll } from '$lib';
</script>

<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<h1>Normal</h1>
<MountOnScroll placeholderSizeProps={{height: 300}} transitionProps={{x: 300, duration: 2000}}>
    <h1>Inisde of a mount on scroll component</h1>
</MountOnScroll>
<MountOnScroll transitionProps={{x: 400, y: -400, duration: 1000}}>
    <h1>Multiple tags inside of a mount on scroll component</h1>
    <h1>This and the above line should render simultaneously</h1>
</MountOnScroll>
<MountOnScroll transitionProps={{x: -200, y: 0, duration: 500, delay: 0}}>
    <h1>This should scroll in from the left</h1>
</MountOnScroll>
<MountOnScroll transitionProps={{x: 0, y: -100, duration: 3000, delay: 0}}>
    <h1>This should slide in really slowly</h1>
</MountOnScroll>
<h1>Normal</h1>

<style>
    h1 {
        border-top: 1px solid black;
    }
</style>