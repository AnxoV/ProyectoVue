<template>
    <div id="tablaUsuarios">
        <div v-if="!usuarios.length" class="alert alert-info" role="alert">
            No existen usuarios
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Nombre</th>
                    <th>Email</th>
                    <th>Ciudad</th>
                    <th>Teléfono</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="usuario in usuarios" :key="usuario.id">
                    <td>
                        {{ usuario.id }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="text" class="form-control" v-model="usuario.name" />
                    </td>
                    <td v-else>
                        {{ usuario.name }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="email" class="form-control" v-model="usuario.email" />
                    </td>
                    <td v-else>
                        {{ usuario.email }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="email" class="form-control" v-model="usuario.address.city" />
                    </td>
                    <td v-else>
                        {{ usuario.address.city }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="email" class="form-control" v-model="usuario.phone" />
                    </td>
                    <td v-else>
                        {{ usuario.phone }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <button class="btn btn-success btn-sm" @click="saveUsuario(usuario)">Guardar</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-info btn-sm" @click="editUsuario(usuario)">Editar</button>
                    </td>
                    <td v-if="editando === usuario.id">
                        <button class="btn btn-secondary btn-sm" @click="cancelEdicion()">Cancelar</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-danger btn-sm" @click="$emit('deleteUsuario', usuario)">Eliminar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "TablaUsuarios",
    props: {
        usuarios: Array
    },
    data() {
        return {
            editando: null,
        }
    },
    methods: {
        editUsuario(usuario) {
            this.usuarioEditado = Object.assign({}, usuario);
            this.editando = usuario.id;
        },
        saveUsuario(usuario) {
            if (!usuario.name.length
            || !usuario.email.length
            || !usuario.address.city
            || !usuario.phone)
                return;
            this.$emit("editUsuario(usuario)");
            this.editando = null;
        },
        cancelEdicion() {
            this.editando = null;
        }
    }
}
</script>

<style scoped>
    
</style>