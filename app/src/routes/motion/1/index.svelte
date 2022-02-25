<script>


    // usually this import strategy should work:
    //import {AnimateSharedLayout,Motion, AnimatePresence} from "svelte-motion";
    import  Motion from 'svelte-motion/src/motion/MotionSSR.svelte';
    import MotionLi from '$lib/motion/MotionLi.svelte';
    let ison = false;
    const list = {
        visible: {
            border: "4px solid white",
            transition: {
                when: "afterChildren",
                staggerChildren: 0.3,
            },
        },
        hidden: {
            border: "0px solid transparent",
            transition: {

                when: "beforeChildren",
            },
        },
    }
    const item = {
        visible: { opacity: 1, x: 0 },
        hidden: { opacity: 0, x: "-50vw" },
    }
    const variants2 = {
        visible: i => ({
            opacity: 1,
            transition: {
                delay: i * 0.3,
            },
        }),
        hidden: { opacity: 0 },
    }

</script>
<style>
    .background{
        background:linear-gradient(250deg, rgb(50,50,255), rgb(150,150,250));;
        display:flex;
        flex-direction:column;
        height:100%;
        justify-content:center;
        align-items:center;
    }
    button {
        border:4px solid white;
        background-color: transparent;
        color: white;
        border-radius:4rem;
        padding:1rem 2rem;
        font-size:200%;
    }
    ul {

        border-radius:4rem;
        padding:2rem 4rem;
    }
    .border{
        border:4px solid white}
</style>
<div class="background">
    <Motion custom={0} let:motion
            variants={variants2}
            initial="hidden"
            animate={!ison?"visible":"hidden"}>
        <ul use:motion class="border">
            {#each [1,2,3] as it(it)}

                <MotionLi variants={variants2} custom={it+1}
                          initial="hidden"
                          animate={!ison?"visible":"hidden"}
                          text={it}/>
            {/each}
        </ul>
    </Motion>
    <Motion initial="hidden" animate={ison?"visible":"hidden"} variants={list} let:motion>
        <ul use:motion >
            <MotionLi variants={item} text="a"/>
            <MotionLi variants={item} text="b"/>
            <MotionLi variants={item} text="c"/>
        </ul>
    </Motion>
    <button on:click={()=>ison=!ison}>click</button>
</div>
