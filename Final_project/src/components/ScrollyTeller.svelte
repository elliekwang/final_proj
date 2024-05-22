<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import Map from "./Map.svelte";
  import { geoMercator } from "d3-geo";
  import Graph from "./Graph.svelte"

  let count, index, offset, progress;
  let width, height;

  let geoJsonToFit = {
    type: "FeatureCollection",
    features: [
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [1, 0],
        },
      },
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [0, 1],
        },
      },
    ],
  };

  $: projection = geoMercator().fitSize([width, height], geoJsonToFit);

</script>

<Scroller
  top={0.0}
  bottom={1}
  threshold={0.5}
  bind:count
  bind:index
  bind:offset
  bind:progress
>
  <div 
    class="background" 
    slot="background"
    bind:clientWidth={width}
    bind:clientHeight={height}
  >
    <Map bind:geoJsonToFit {index} />
    <Graph {index} {width} {height} {projection} />
  </div>

  <div class="foreground" slot="foreground">
    <section>Hi, This is a website dedicated to teach you how to chose the best houses in Los Angeles using data from Airbnb.</section>
    <section>This is the second section.</section>
    <section>This is the third section.</section>
    <section>This is the fourth section.</section>
    <section>This is the fifth section.</section>
    <section>This is the sixth section.</section>
  </div>
</Scroller>

<style>
  .background {
    width: 100%;
    height: 0vh;
    position: relative;
    outline: rgb(0, 119, 0) solid 3px;
  }

  .foreground {
    width: 90%;
    margin: 0 auto;
    height: auto;
    position: relative;
    outline: rgb(255, 255, 255) solid 3px;
  }

  section {
    height: 80vh;
    background-color: rgba(0, 0, 0, 0.2); /* 20% opaque */
    /* color: white; */
    outline: rgb(212, 212, 212) solid 3px;
    text-align: center;
    max-width: 750px; /* adjust at will */
    color: black;
    padding: 1em;
    margin: 0 0 2em 0;
  }
</style>
