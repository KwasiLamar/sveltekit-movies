<script context="module">
  const key = import.meta.env.VITE_API;

  export async function load({ fetch }) {
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/popular?api_key=${key}&language=en-US&page=1`
    );
    const movies = await res.json();

    if (res.ok) {
      return {
        props: { popular: movies.results },
      };
    }
  }
</script>

<script>
  import global from "../styles/global.css";
  import { fly } from "svelte/transition";
  export let popular;
  import PopularMovies from "../components/PopularMovies.svelte";
  import SearchMovies from "../components/SearchMovies.svelte";
</script>

<div in:fly={{ y: 50, duration: 500 }} out:fly={{ duration: 500 }}>
  <SearchMovies />
  <PopularMovies movies={popular} />;
</div>
