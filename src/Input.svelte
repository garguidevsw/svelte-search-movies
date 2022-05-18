
<script>
    import Movie from './movie.svelte';

    let value = "";
    let response = [];

    const handleInput = (event) => {
        value = event.target.value;
    }

    $: if(value.length > 2){
        
        response = fetch(`http://www.omdbapi.com/?s=${value}&apikey={yourAPIKEY}`)
            // .then(res => !res.ok() && new Error('Something bad happened with the fetching of movies'))
            .then( res => res.json())
            .then(apiResponse => response = apiResponse.Search || [])
    }

</script>

<input placeholder="Search movie" value={value} on:input={handleInput} type="text">

{#await response}
    <strong>Loading....</strong>
{:then movies}
    {#each movies as { Title, Poster, Year}}
        <Movie title={Title} poster={Poster} year={Year}></Movie>
    {:else}
        <strong>No hay resultados</strong>
    {/each}
{:catch error}
    <p>❌ There has been an error</p>
{/await}
