<script lang="ts">
  import "./app.css";

  const randomPokemon = async () => {
    const response = await fetch("https://pokeapi.co/api/v2/pokemon/");
    const data = await response.json();

    const rando = Math.round(Math.random() * data.results.length);
    return data.results[rando];
  };

  let promise;

  const handleClick = () => {
    promise = randomPokemon();
  };
</script>

<main class="min-h-screen grid place-items-center">
  <div class="flex flex-col items-center justify-center gap-8">
    <div>
      <h1 class="text-2xl font-bold">Choose Your Pokémon</h1>
    </div>
    {#await promise}
      <p>Loading...</p>
    {:then data}
      {#if data}
        <a class="text-lg" href={data.url}>{data.name}</a>
      {/if}
    {:catch error}
      <p>{error}</p>
    {/await}
    <button class="p-2 bg-blue-500 text-white rounded" on:click={handleClick}
      >Random Your Pokémon</button
    >
  </div>
</main>
