<script>
    import { Link } from "svelte-routing";
</script>

<style>
    /* Basic styling */
    * {
        box-sizing: border-box;
    }
    nav {
        background: #E0E0E0;
        padding: 8px;
        position: -webkit-sticky; /* Safari */
        position: sticky;
        top: 0;
        width: 100%;
    }
    ul {
        list-style-type: none;
    }
    .menu li:hover {
        text-shadow: 3px 3px 4px #6f6f70;
    }
    .menu li {
        font-weight: bold;
        font-size: 16px;
        padding: 15px 5px;
        white-space: nowrap;
    }
    /* Móvil */
    .menu {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: center;
    }
    .item {
        width: 100%;
        text-align: center;
        order: 3;
        display: none;
    }
    .active {
        display: block;
    }
    /* Tablet */
    @media all and (min-width: 600px) {
        .menu {
            justify-content: center;
        }
        .logo {
            flex: 1;
        }
        .item {
            order: 1;
            display: block;
            width: auto;
        }
    }
    /* PC */
    @media all and (min-width: 900px) {
        .item {
            order: 1;
            display: block;
            width: auto;
        }
        .logo {
            order: 0;
        }
        .menu li {
            padding: 15px 10px;
        }
    }
</style>

<nav>
    <ul class="menu">
        <li class="logo">
            <Link to="/">🏥 Inicio</Link>
        </li>
        <li class="item active">
            <Link to="/doctores">👨‍⚕️ Doctores</Link>
        </li>
        <li class="item active">
            <Link to="/pacientes">😷 Pacientes</Link>
        </li>
    </ul>
</nav>