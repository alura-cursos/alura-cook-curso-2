<script lang="ts">
    import '../app.css';

    import Cabecalho from '$lib/components/Cabecalho.svelte';
    import MinhaLista from '$lib/components/MinhaLista.svelte';
    import Titulo from '$lib/components/Titulo.svelte';

    import categorias from '$lib/json/categorias.json';
    import Categoria from '$lib/components/Categoria.svelte';
    import Tag from '$lib/components/Tag.svelte';
    import Rodape from '$lib/components/Rodape.svelte';
    
    let minhaLista: string[] = [];

    function adicionarIngrediente(evento: CustomEvent<string>) {
        const ingrediente = evento.detail;
        minhaLista = [...minhaLista, ingrediente];
    }

    function removerIngrediente(evento: CustomEvent<string>) {
        const ingrediente = evento.detail;
        minhaLista = minhaLista.filter(
            (item) => item !== ingrediente
        );
    }
</script>

<svelte:head>
    <title>Alura Cook</title>
</svelte:head>

<div class="container-principal">
    <Cabecalho />
    
    <div class="estilo-principal">
        {#if minhaLista.length}
            <div class="minha-lista-container">
                <MinhaLista ingredientes={minhaLista} />

                <div class="divisoria"></div>
            </div>
        {/if}
        
        <main>
            <Titulo tag='h1'>Ingredientes</Titulo>

            <div class="info">
                <p>Selecione abaixo os ingredientes que você deseja usar nesta refeição:</p>
                <p>*Atenção: consideramos que você tenha em casa sal, pimenta e água.</p>
            </div>

            <ul class="categorias">
                {#each categorias as categoria (categoria.nome)}
                    <li>
                        <Categoria
                            {categoria}
                            on:adicionarIngrediente={adicionarIngrediente}
                            on:removerIngrediente={removerIngrediente}
                        />
                    </li>
                {/each}
            </ul>

            <div class="buscar-receitas">
                <a href="/receitas">
                    <Tag ativa={true} tamanho="lg">Buscar Receitas!</Tag>
                </a>
            </div>
        </main>
    </div>

    <Rodape />
</div>

<style>
    .container-principal {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }
 
    .estilo-principal {
        text-align: center;
        padding: 0 5vw 3.375rem;
        flex: 1;
    }
 
    .minha-lista-container {
        margin-bottom: 2rem;
    }

    .divisoria {
        width: 40vw;
        height: 2px;
        background-color: var(--verde);
        margin: 0 auto;
    }
 
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