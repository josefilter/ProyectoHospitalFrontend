<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Doctor                from "./Doctor.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let doctor = {};

  onMount(async () => {
    const response = await fetch(URL.doctores);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>DOCTORES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Doctor bind:doctor>
    <div style="text-align: right">
      <Boton documento={doctor} tipo="insertar" coleccion="doctores" />
    </div>
  </Doctor>
</div>

<div class="container">
  {#each datos as doctor}
    <doctor {doctor}>
      <div style="text-align: right">
        <Boton documento={doctor} tipo="modificar" coleccion="doctores" />
        <Boton documento={doctor} tipo="eliminar"  coleccion="doctores" />
      </div>
    </doctor>
  {/each}
</div>