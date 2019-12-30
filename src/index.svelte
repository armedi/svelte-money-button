<script>
  const propsList = [
    "to",
    "amount",
    "currency",
    "label",
    "successMessage",
    "opReturn",
    "outputs",
    "cryptoOperations",
    "clientIdentifier",
    "buttonId",
    "buttonData",
    "type",
    "onPayment",
    "onCryptoOperations",
    "onError",
    "onLoad",
    "editable",
    "disabled",
    "devMode"
  ];

  let moneyButton;
  let moneyButtonLoaded = false;

  function handleScriptLoad(event) {
    const options = Object.entries($$props)
      .filter(([k]) => propsList.indexOf(k) !== -1)
      .reduce((a, [k, v]) => Object.assign({}, a, { [k]: v }), {});

    options.onLoad = (e) => {
      if (typeof $$props.onLoad === 'function') {
        $$props.onLoad()
      }
      moneyButtonLoaded = true
    }

    window.moneyButton.render(moneyButton, options);
  }
</script>

<style>
  .moneybutton {
    height: 50px;
    width: 280px;
  }

  .hidden {
    display: none;
  }

  .outer {
    background-color: #f2efef;
    width: 196px;
    height: 50px;
    padding: 5px;
    border: 1px solid #dad8d8;
    border-radius: 50px;
  }

  .inner {
    color: #666464;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    font-family: "IBM Plex Sans", sans-serif;
    font-size: 14px;
    font-weight: bold;
    background-color: #fcfcfc;
    height: 100%;
    padding: 5px;
    border: 1px solid #4772f6;
    border-radius: 20px;
  }

  .spinner {
    width: 40px;
    height: 40px;
    margin-right: 1rem;
    background-color: #4772f6;
    border-radius: 100%;
    -webkit-animation: sk-scaleout 1s infinite ease-in-out;
    animation: sk-scaleout 1s infinite ease-in-out;
  }

  @-webkit-keyframes sk-scaleout {
    0% {
      -webkit-transform: scale(0);
    }
    100% {
      -webkit-transform: scale(1);
      opacity: 0;
    }
  }

  @keyframes sk-scaleout {
    0% {
      -webkit-transform: scale(0);
      transform: scale(0);
    }
    100% {
      -webkit-transform: scale(1);
      transform: scale(1);
      opacity: 0;
    }
  }
</style>

<svelte:head>
  <script
    on:load={handleScriptLoad}
    defer
    src="https://www.moneybutton.com/moneybutton.js">

  </script>
</svelte:head>

<div class="moneybutton">
  <div class:hidden={!moneyButtonLoaded}>
    <div bind:this={moneyButton} />
  </div>
  {#if !moneyButtonLoaded}
    <slot>
      <div class="outer">
        <div class="inner">
          <span class="spinner" />
          <p>loading...</p>
        </div>
      </div>
    </slot>
  {/if}
</div>
