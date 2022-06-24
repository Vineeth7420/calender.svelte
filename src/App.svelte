
<script>
 import Calender from "./Components/Calender.svelte";
 import ToDolist from "./Components/To-dolist.svelte";

let schedulerShowing = false

</script>

<main>

<Calender on:click= {() =>schedulerShowing = true}/>
{#if schedulerShowing}
	<ToDolist on:click = {() => schedulerShowing = false} />
{/if}


</main>

<style>
main {font-family: Verdana, sans-serif;}
</style>