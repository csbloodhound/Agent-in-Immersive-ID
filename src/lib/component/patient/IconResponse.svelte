<script>
    export let circle_text;
    export let initial_prompt;
</script>

<div class="icon-plus-response-wrapper">
    <div class="circle">
      {circle_text}
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

    div.circle {
    background-color: #F5EADC; 
    border-radius: 50%; 
    width: 200px; 
    height: 200px; 
    display: flex; 
    align-items: center; 
    justify-content: center; 
    font-family: Inter;
    color: #0D3C26;
    font-size: 40px; 
    font-weight: 600;
  }

  div.gpt-response {
    color: #0D3C26;
    font-family: Inter;
    font-size: 14px;
    font-style: normal;
    font-weight: 600;
    line-height: 150%;
  }
</style>