<script context="module">
  const key = import.meta.env.VITE_API;
  export async function load({ fetch, params }) {
    const movie_id = params.id;
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/${movie_id}popular?api_key=${key}&language=en-US&page=1`
    );
    const movieDetail = await res.json();

    if (res.ok) {
      return {
        props: { movieDetail },
      };
    }

    return {
      status: res.status,
      error: new Error("Could not fetch that guide"),
    };
  }
</script>

<script>
  import { fly } from "svelte/transition";
  export let movieDetail;
</script>

<div
  class="movie-details"
  in:fly={{ y: 50, duration: 500 }}
  out:fly={{ duration: 500 }}
>
  <div class="img-container">
    <img
      src={`https://image.tmdb.org/t/p/original/${movieDetail.backdrop_path}`}
      alt={movieDetail.title}
    />
    <div class="txt-container">
      <h1>{movieDetail.title}</h1>
      <p class="overview">{movieDetail.overview}</p>
      <p>
        <span>Release Date: </span>{movieDetail.release_date}<br />
        <span> Budget: </span>${movieDetail.budget
          .toString()
          .replace(/\B(?=(\d{3})+(?!\d))/g, ",")}<br />
        <span>Rating: </span>{parseFloat(
          movieDetail.vote_average.toString()
        )}<br />
      </p>
    </div>
  </div>
</div>

<style>
  h1 {
    padding: 1rem 0rem 2rem;
  }

  p {
    padding: 1rem 0rem;
  }

  .img-container {
    width: 100%;
  }

  img {
    border-radius: 1rem;
    width: 100%;
  }

  .movie-details {
    margin: 2rem 20%;
  }

  span {
    font-weight: bold;
  }
</style>
