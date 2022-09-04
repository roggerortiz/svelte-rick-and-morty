<script>
  let characters = [];
  let paginate = {
    count: 0,
    pages: 1,
    next: "",
    prev: "",
  };

  async function fetchCharacters() {
    const response = await fetch("https://rickandmortyapi.com/api/character");
    const data = await response.json();
    characters = data.results;
    paginate = data.info;
  }

  fetchCharacters();
</script>

<main>
  <h1>Rick And Morty Characters</h1>
  <div>
    {#each characters as character}
      <div>
        <h2>{character.name}</h2>
        <h3>{character.species}</h3>
        <img src={character.image} alt={character.name} />
      </div>
    {/each}
  </div>
</main>
