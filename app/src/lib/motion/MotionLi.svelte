<script>
    import  Motion from 'svelte-motion/src/motion/MotionSSR.svelte';

    export let variants,
        initial=undefined,
        custom=undefined,
        animate=undefined,
        text="";

</script>
<style>
    li{
        font-size:200%;
        color:white;
    }
</style>
<Motion let:motion {variants} {initial} {animate} {custom}>
    <li use:motion>{text}</li>
</Motion>
