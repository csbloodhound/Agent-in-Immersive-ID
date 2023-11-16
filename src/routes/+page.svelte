<script>
    import { fade } from 'svelte/transition';
    import { base } from '$app/paths';
</script>


<div in:fade={{ duration: 500 }}>
    <div class="big-wrap">
        <h1>
            Hi there! This is a Demo of AI Agent in immersive interaction.
        </h1>
        <div class="role-options">
            <a href="{base}/demo">
                <button class="role-button">Start the Demo</button>
            </a>
        </div>
    </div>
</div>

<style>
    :global(body) {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh; 
        margin: 0;
        background: #F9F3EB;
    }

    a {
        text-decoration: none;
    }

    div.big-wrap {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 30px;
        color: #0D3C26;
        font-family: Inter;
        font-size: 16px;
        font-weight: 100;
        line-height: 100%;
    }

    div.role-options {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 25px;
    }

    button.role-button {
        display: flex;
        width: auto;
        padding: 23px 40px;
        justify-content: center;
        align-items: center;
        gap: 10px;
        border: none;

        border-radius: 4px;
        background: #F5EADC;

        color: #0D3C26;
        font-family: Inter;
        font-size: 24px;
        font-style: italic;
        font-weight: 600;
        line-height: 100%; /* 30px */
    }

    button.role-button:hover {
        box-shadow: 0px 0px 8px rgba(50, 46, 42, 0.10);
        cursor: pointer;
    }
</style>