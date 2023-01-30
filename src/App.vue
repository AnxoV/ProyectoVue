<template>
    <div id="app" class="container">
        <div class="row">
            <div class="col-md-12 mt-2">
                <h1>GESTIÓN CLIENTES</h1>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12 mt-2">
                <TablaUsuarios :usuarios="usuarios" @deleteUsuario="deleteUsuario" @editUsuario="editUsuario" />
            </div>
        </div>
        <div class="row">
            <div class="col-md-12 mt-2">
                <h1>FORMULARIO CLIENTES</h1>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12 mt-2">
                <FormularioUsuario :usuarios="usuarios" @deleteUsuario="deleteUsuario" @editUsuario="editUsuario" />
            </div>
        </div>
    </div>
</template>

<script>
import TablaUsuarios from "./components/TablaUsuarios.vue";
import FormularioUsuario from "./components/FormularioUsuario.vue";

export default {
    name: "App",
    components: {
        TablaUsuarios,
        FormularioUsuario
    },
    data() {
        return {
            usuarios: []
        }
    },
    methods: {
        async postUsuarios(usuario) {
            try {
                const response = await fetch("http://localhost:3000/usuarios", {
                    method: "POST",
                    body: JSON.stringify(usuario),
                    headers: {
                        "Content-type": "application/json; charset=UTF-8"
                    }
                });
                const usuarioAlta = await response.json();
                this.usuarios.push(usuarioAlta);
            } catch (error) {
                console.warn(error);
            }
        },
        async getUsuarios() {
            try {
                const response = await fetch("http://localhost:3000/usuarios");
                this.usuarios = await response.json();
            } catch (error) {
                console.warn(error);
            }
        },
        async deleteUsuario(usuario) {
            console.log(usuario);
            try {
                await fetch(`http://localhost:3000/usuarios/${usuario.id}`, {
                    method: "DELETE"
                });

                this.usuarios = this.usuarios.filter(usr => usr.id != usuario.id);
            } catch(error) {
                console.log(error);
            }
        },
        async editUsuario(usuario) {
            console.log(usuario);
        },
        async guardarUsuario(usuario) {
            console.log(usuario);
        },
        async cancelarEdicion(usuario) {
            console.log(usuario);
        }
    },
    mounted() {
        this.getUsuarios();
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
