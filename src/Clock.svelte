<script>
  let t = +new Date();
  let now = +new Date();
  let timer;

  let laps = [];

  $: tick = now - t;
  $: sec = ((tick / 1000) % 60).toFixed(2).padStart(5, "0");
  $: min = ((tick / 1000 / 60) % 60).toFixed(0).padStart(2, "0");
  $: hour = ((tick / 1000 / 60 / 24) % 24).toFixed(0).padStart(2, "0");

  const 시작 = () => {
    laps = [];
    t = +new Date();
    timer = setInterval(() => (now = +new Date()), 10);
  };

  const 종료 = () => {
    clearInterval(timer);
  };

  const LAP = () => {
    laps = [...laps, `${hour}:${min}:${sec}`];
  };
</script>

<div class="clock">
  <div>{hour}:{min}:{sec}</div>
</div>

<button on:click={시작}>시작</button>
<button on:click={종료}>종료</button>
<button on:click={LAP}>LAP</button>

{#each laps as lap, index}
  <div>
    <div>LAP {index + 1}</div>
    <div>{lap}</div>
  </div>
{/each}

<style>
  .clock {
    width: 300px;
    height: 300px;
    background: #ffc0cb;
    color: #000;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 30px;
    font-weight: 100;
    font-family: monospace;
  }
</style>
