<script>
    export let vis_text = "Hi there!";
    export let initial_prompt = "I am Ready to Assist You!";
    export let isText = true;
    export let image_url;
</script>

<div class="icon-plus-response-wrapper">
    <div class="vis">
      {#if isText}
        {vis_text}
      {:else}
        <img src={image_url} alt="visualization">
      {/if}
    </div>
    <div class="gpt-response">
      {initial_prompt}
    </div>
</div>

<style>
    div.icon-plus-response-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 24px;
        flex: 1 0 0;
        align-self: stretch;
    }

    div.vis {
        display: flex;
        width: 300px;
        height: 200px;
        justify-content: center;
        align-items: center;
        gap: 10px;
        border-radius: 6px;
        background: #F5EADC;
        color: #0D3C26;
        font-family: Inter;
        font-size: 40px;
        font-weight: 600;
        line-height: 100%; /* 30px */
    }

    div.gpt-response {
        color: #0D3C26;
        font-family: Inter;
        font-size: 14px;
        font-style: normal;
        font-weight: 600;
        line-height: 150%; /* 21px */
    }


    div.vis img {
        width: 100%;
        height: auto;
    }
</style>