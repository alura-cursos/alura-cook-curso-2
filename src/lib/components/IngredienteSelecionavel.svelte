<script lang="ts">
    import { minhaLista } from "$lib/stores/minhaLista";

    import Tag from "./Tag.svelte";

    export let ingrediente: string;

    let selecionado = false;

    function aoClicar() {
        if (!selecionado) {
            $minhaLista = [...$minhaLista, ingrediente];
        } else {
            $minhaLista = $minhaLista.filter(
                (item) => item !== ingrediente
            );
        }
    }
</script>

<button on:click={aoClicar}>
    <Tag ativa={selecionado}>{ingrediente}</Tag>
</button>

<style>
    button {
        cursor: pointer;
    }
</style>