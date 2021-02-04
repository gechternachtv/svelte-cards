<script>
    export let name = 'no name';
    export let tags = [];
    export let color = 'rgb(214, 194, 194)';
</script>

<main style="background-color:{color}">
    {#each tags as tag}
        <button class="tag">{tag}</button>
    {/each}
    <h2>{name}</h2>

</main>

<style lang="scss">
    main {
        max-width:300px;
        border-radius:10px;
        padding:20px;
        margin:auto;
        width:100%;
        height:100%;
    }
    .tag{
        font-size:12px;
        border-radius:10px;
        margin:5px;
    }
</style>
