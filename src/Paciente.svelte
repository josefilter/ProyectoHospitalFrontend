<script>    
    import Boton from "./Boton.svelte";

    export let paciente = {};
</script>

<style>
    .title {
        font-weight: bold;
    }
    .campo {
        background: #D4D4D4;
    }
    .card {
        background-color: #E0E0E0;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        border-radius: 5px;
        transition: 0.3s;
        padding: 10px;
        margin: 10px;
    }
    .card:hover {
        box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.4);
    }
    input {
        background-color: inherit;
        padding: 10px;
        font-size: 14px;
        color: black;
        border: 0;
        outline: none;
        margin-left: 5px;
        margin-bottom: 4px;
        max-width: 140px;
    }
    input:focus {
        background-color: #D4D4D4;
    }
    input:required:invalid,
    input:focus:invalid {
        background-color: #CBCBCB;
    }
</style>

<div class="card" on:click>
    <input bind:value={paciente.nombre} class="title campo" />
    <input bind:value={paciente.apellidos} class="title campo" />
    <input bind:value={paciente.telefono} class="title campo" />
    <input bind:value={paciente.enfermedad} class="title campo" />
    <slot />
</div>