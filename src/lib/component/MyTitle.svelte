<script>
    export let title;
    export let status = "inactive";

    $: status;
</script>

<h1 class={status == "inactive" ? "title-inactive" : "title-acitve"}>
        {title}
</h1>


<style>
    h1.title-inactive {
        color: rgba(13, 60, 38, 0.30);
        font-family: Inter;
        font-size: 24px;
        font-style: italic;
        font-weight: 600;
        line-height: 100%; /* 24px */
    }

    h1.title-acitve {
        color: rgba(13, 60, 38);
        font-family: Inter;
        font-size: 24px;
        font-style: italic;
        font-weight: 600;
        line-height: 100%; /* 24px */
    }
</style>