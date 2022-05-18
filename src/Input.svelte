
<script>
    import Movie from './movie.svelte';

    let value = "";
    let loading = false;
    let response = [];

    const handleInput = (event) => {
        value = event.target.value;
    }

    $: if(value.length > 2){
        loading = true;
        fetch(`http://www.omdbapi.com/?s=${value}&apikey=c27398bd`)
            .then( res => res.json())
            .then(apiResponse => {
                response = apiResponse.Search || [];
                console.log(apiResponse);
                loading = false;
            })
    }

</script>

<input placeholder="Search movie" value={value} on:input={handleInput} type="text">

{#if loading}
    <strong>Loading....</strong>
{:else}
    {#each response as { Title, Poster, Year}}
        <Movie title={Title} poster={Poster} year={Year}></Movie>
    {:else}
        <strong>No hay resultados</strong>
    {/each}

{/if}
