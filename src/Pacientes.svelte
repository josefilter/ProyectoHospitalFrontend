<script>
    import { onMount, getContext } from "svelte";
    import { jsonData }            from "./store.js";

    import Buscar                  from "./Buscar.svelte";
    import Paciente                 from "./Paciente.svelte";
    import Boton                   from "./Boton.svelte";

    const URL = getContext("URL");

    let busqueda = "";
    let paciente = {};

    onMount(async () => {
        const response = await fetch(URL.pacientes);
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

<h1>PACIENTES</h1>
<Buscar bind:busqueda />

<div class="container">
    <Paciente bind:paciente>
        <div style="text-align: right">
            <Boton documento={paciente} tipo="insertar" coleccion="pacientes" />
        </div>
    </Paciente>
</div>

<div class="container">
    {#each datos as paciente}
        <Paciente {paciente}>
            <div style="text-align: right">
                <Boton documento={paciente} tipo="modificar" coleccion="pacientes" />
                <Boton documento={paciente} tipo="eliminar" coleccion="pacientes" />
            </div>
        </Paciente>
    {/each}
</div>