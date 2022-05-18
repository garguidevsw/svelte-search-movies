<script>
	export let initialCounter = 0;
    export let maxCounter = 0;

	let counter = initialCounter;

	
	function handleClick(){
		counter++;
	}

    $: isEvenOrOdd = counter % 2 === 0 ? 'Is Even' : 'Is Odd';

    // $: {
    //     if(counter > 9){
    //         counter = 9;
    //     }
    // }
    $: if(counter > maxCounter){
        counter = maxCounter;
    }
    

</script>

<main>
	<h1>Contador: {counter}!</h1>
    <span>{isEvenOrOdd}</span>
	
	<button on:click={handleClick}>Incrementar</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>