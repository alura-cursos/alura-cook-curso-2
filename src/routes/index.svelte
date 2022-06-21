<script lang="ts">
    import Titulo from "$lib/components/compartilhados/Titulo.svelte";
    import Categoria from "$lib/components/paginas/index/Categoria.svelte";

    import categorias from "$lib/json/categorias.json";

    import { minhaLista } from "$lib/stores/minhaLista";
    import { beforeNavigate } from "$app/navigation";
    import TagLink from "$lib/components/compartilhados/TagLink.svelte";

    $: listaVazia = $minhaLista.length === 0;

    beforeNavigate((navigation) => {
        if (listaVazia && navigation.to?.pathname === '/receitas') {
            navigation.cancel();
        }
    })
</script>

<svelte:head>
    <title>Alura Cook</title>
</svelte:head>

<main>
    <Titulo tag="h1">Ingredientes</Titulo>

    <div class="info">
        <p>
            Selecione abaixo os ingredientes que você deseja usar nesta
            refeição:
        </p>
        <p>
            *Atenção: consideramos que você tenha em casa sal, pimenta e água.
        </p>
    </div>

    <ul class="categorias">
        {#each categorias as categoria (categoria.nome)}
            <li>
                <Categoria
                    {categoria}
                />
            </li>
        {/each}
    </ul>

    <div class="buscar-receitas">
        <TagLink href="/receitas" desabilitada={listaVazia}>
            Buscar receitas!
        </TagLink>
    </div>
</main>

<style>
    .info {
        margin-bottom: 3.375rem;
    }

    .info > p {
        line-height: 2rem;
    }

    .categorias {
        margin-bottom: 4.6875rem;

        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1.5rem;
    }

    .buscar-receitas {
        display: flex;
        justify-content: center;
    }
</style>
