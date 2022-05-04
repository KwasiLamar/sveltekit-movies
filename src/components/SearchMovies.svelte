<script>
  import { goto } from "$app/navigation";
  import { fly } from "svelte/transition";
  let inputValue = "";
  let active = false;

  function submitSearch() {
    active = true;
    goto(`/search/${inputValue}`);
  }
</script>

<form class="search" on:submit|preventDefault={submitSearch}>
  {#if !active}
    <label
      in:fly={{ y: -10, duration: 500 }}
      out:fly={{ y: -10, duration: 500 }}
      for="search-movie">Search</label
    >
  {/if}
  <input
    on:blur={() => (active = false)}
    on:focus={() => (active = true)}
    type="text"
    bind:value={inputValue}
    name="search-movie"
    class:selected={active}
  />
  {#if inputValue}
    <button in:fly={{ y: 0, duration: 500 }} out:fly={{ y: 0, duration: 500 }}
      >Search</button
    >
  {/if}
</form>

<style>
  .search {
    margin: 1rem;
    position: relative;
    width: 30%;
  }

  button {
    font-size: 0.7rem;
    padding: 0rem 1rem;
    background: rgb(96, 110, 201);
    color: #fff;
    font-weight: bold;
    border: none;
    position: absolute;
    bottom: 50%;
    right: 0;
    transform: translate(0, 50%);
    height: 100%;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    cursor: pointer;
    font-family: "Poppins", sans-serif;
  }

  label {
    position: absolute;
    font-size: 0.8rem;
    top: 50%;
    left: 0;
    transform: translate(0, -50%);
    pointer-events: none;
    color: #fff;
    padding: 0rem 1rem;
  }

  input {
    width: 100%;
    border: none;
    font-size: 1rem;
    font-family: "Poppins", sans-serif;
    outline: none;
    color: #fff;
    padding: 0.5rem 0.1rem;
    transition: background 0.75s ease-out;
    background: rgb(63, 63, 63);
    font-weight: bold;
    border-radius: 10px;
    padding: 1rem;
  }

  input.selected {
    background: rgb(50, 50, 50);
  }
</style>
