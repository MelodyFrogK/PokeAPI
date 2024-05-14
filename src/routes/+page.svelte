<script>
    // pokestore에서 arrPokemon 가져오기
    import { arrPokemon } from '../stores/pokestore';
    //console.log($arrPokemon);
    import PokemonCard from '../components/pokemonCard.svelte';

    //검색창
    let searchTerm = '';
    let filteredPokemon = [];

    // reactivity($: 삽입시, 안에 삽입되는 내용이 변경될때마다 출력해줌)
    $: {
      console.log(searchTerm);
      if (searchTerm) {
        filteredPokemon = $arrPokemon.filter((pokemon) => pokemon.name.includes(searchTerm));
      } else {
        filteredPokemon = [...$arrPokemon];
      }
    }
</script>

<svelte:head>
    <title>포켓몬 위키</title>
</svelte:head>


<h1 class="text-4xl text-center my-8 font-bold underline">
    포켓몬 위키 사이트
</h1>

<input class = "w-full p-4 rounded-md mb-8 text-lg border-2 border-gray-200" type="text" bind:value={searchTerm} placeholder="포켓몬 검색"/>


<div class = "grid gap-4 md:grid-cols-3 grid-cols-2">
  {#each filteredPokemon as pokemon}
    <PokemonCard {pokemon} />
  {/each}
</div>
