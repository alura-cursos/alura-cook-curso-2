<script lang="ts">
    import Tag from "./Tag.svelte";

    export let href: string;
    export let desabilitada = false;
</script>

<a {href}>
    <Tag ativa={true} tamanho="lg" {desabilitada}>
        <slot></slot>
    </Tag>
</a>
