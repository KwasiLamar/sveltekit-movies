<script context="module">
  const key = import.meta.env.VITE_API;
  export async function load({ fetch, params }) {
    const res = await fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=${key}&language=en-US&query=${params.id}&page=1&include_adult=true`
    );
    const data = await res.json();
    console.log(data);

    if (res.ok) {
      return {
        props: { searchedMovie: data.results },
      };
    }

    return {
      status: res.status,
      error: new Error("Could not fetch that guide"),
    };
  }
</script>

<script>
  import MovieCard from "../../components/MovieCard.svelte";

  export let searchedMovie;
</script>

<div class="searched-movies">
  {#each searchedMovie as movie}
    <MovieCard {movie} />
  {/each}
</div>

<style>
  .searched-movies {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-column-gap: 1rem;
    grid-row-gap: 2rem;
  }
</style>
