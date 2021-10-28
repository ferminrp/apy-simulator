<script>
  let mode = "input";
  let capital = 3000;
  let apy = 0.15;
  let final;
  let timer;
  let initial_date;

  function start() {
    initial_date = new Date();
    mode = "simular";
    final = capital;
    timer = setInterval(function () {
      let now = new Date();
      // miliseconds between initial and now
      let diff = now.getTime() - initial_date.getTime();
      final = capital * Math.pow(1 + apy / 365, diff / (1000 * 60 * 60 * 24));
    }, 10);
  }

  function formatNums(num, sep, dec, u) {
    sep = sep || ",";
    u = u || "\\d";
    if (typeof num != "string") {
      num = String(num);
      if (dec && dec != ".") num = num.replace(".", dec);
    }
    return num.replace(
      RegExp(
        "\\" +
          (dec || ".") +
          u +
          "+|" +
          u +
          "(?=(?:" +
          u +
          "{3})+(?!" +
          u +
          "))",
        "g"
      ),
      function (a) {
        return a.length == 1 ? a + sep : a;
      }
    );
  }
</script>

<main>
  {#if mode == "input"}
    <div class="form-container">
      <label for="capital">How much DAI do you have?</label>
      <input id="capital" type="number" bind:value={capital} />
      <label for="apy">What's the APY you are getting?</label>
      <input id="apy" type="number" bind:value={apy} />
      <button on:click={start}>Start</button>
    </div>
  {:else}
    <div class="form-container">
      <h2>${final}</h2>
    </div>
  {/if}
</main>

<style>
  label {
    font-weight: bold;
  }
  input {
    border: 1px solid #e2e2e2;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.05) 0 2px 2px;
    box-sizing: border-box;
    color: #000;
    cursor: text;
    font-family: Inter, sans-serif;
    font-size: 16px;
    margin: 0 0 1rem 0;
    padding: 0.4em;
    width: 100%;
  }

  .form-container {
    box-shadow: rgba(0, 0, 0, 0.05) 0 2px 2px;
    width: 450px;
    max-width: 90vw;
    background-color: white;
    margin: 3rem auto;
    padding: 3rem;
    border-radius: 0.5rem;
	box-sizing: border-box;
  }

  button {
    background-color: #3d6e70;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    color: #fff;
    cursor: pointer;
    font-family: Inter, sans-serif;
    font-size: 16px;
    margin: 1rem 0 0.5em;
    outline: none;
    padding: 0.5rem 0.4em;
    text-align: center;
    width: 100%;
  }

  h2 {
    font-size: 1.2rem;
    font-weight: 600;
  }
</style>
