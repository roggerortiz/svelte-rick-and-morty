<script>
import Character from "./lib/Character.svelte";

  let isLoading = true;
  let characters = [];
  let pagination = {};
  let page = 1;

  async function fetchCharacters() {
    characters = [];
    isLoading = true;

    const response = await fetch(
      `https://rickandmortyapi.com/api/character/?page=${page}`
    );
    const data = await response.json();
    characters = data.results;
    pagination = data.info;
    isLoading = false;
    console.log(characters);
  }

  function previousPage() {
    page--;
    fetchCharacters();
  }

  function nextPage() {
    page++;
    fetchCharacters();
  }

  fetchCharacters();
</script>

<div class="container py-4">
  <div class="border-bottom mb-3 py-3 text-white text-center">
    <h2 class="m-0">Rick and Morty</h2>
  </div>

  <div class="characters">
    {#if !isLoading}
      <div class="row">
        {#each characters as character}
          <div class="col-sm-6 col-md-4 col-xl-3 pt-4">
            <Character character={character} />
          </div>
        {/each}
      </div>
    {:else}
      <div class="d-flex justify-content-center align-items-center h-100">
        Loading...
      </div>
    {/if}
  </div>

  <div
    class="d-flex justify-content-center align-items-center border-top mt-3 py-3"
  >
    <nav>
      <ul class="pagination m-0">
        <li class={`page-item${page === 1 ? " disabled" : ""}`}>
          <button class="page-link" on:click={previousPage}>{`<<`}</button>
        </li>
        <li class="page-item disabled" aria-current="page">
          <button class="page-link text-dark"
            >Page {page} of {pagination.pages}</button
          >
        </li>
        <li class={`page-item${page === pagination.pages ? " disabled" : ""}`}>
          <button class="page-link" on:click={nextPage}>{`>>`}</button>
        </li>
      </ul>
    </nav>
  </div>
</div>

<style>
  .container {
    height: 100vh;
  }

  .row {
    margin-top: -1.5rem;
  }

  .characters {
    height: calc(100vh - 198px);
    min-height: calc(100vh - 198px);
    max-height: calc(100vh - 198px);
    overflow-y: auto;
    overflow-x: hidden;
  }
</style>
