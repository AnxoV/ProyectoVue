<template>
    <div id="formularioUsuario">
        <form @submit.prevent="enviarFormulario">
            <div class="container">
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Nombre</label>
                            <input
                                ref="name"
                                v-model="usuario.name"
                                type="text"
                                class="form-control"
                                :class="{'isInvalid': procesando && nameInvalido}"
                                @focus="resetEstado"
                                @keypress="resetEstado" />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Email</label>
                            <input
                                v-model="usuario.email"
                                type="email"
                                class="form-control"
                                :class="{'isInvalid': procesando && emailInvalido}"
                                @focus="resetEstado"
                                @keypress="resetEstado" />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Teléfono</label>
                            <input
                                v-model="usuario.phone"
                                type="text"
                                class="form-control"
                                :class="{'isInvalid': procesando && phoneInvalido}"
                                @focus="resetEstado"
                                @keypress="resetEstado" />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <input
                                type="button"
                                value="Añadir"
                                class="btn btn-success"
                                @click="enviarFormulario()"/>
                        </div>
                    </div>
                </div>
            </div>
            <div class="container">
                <div class="row">
                    <div class="col-md-12">
                        <div v-if="error && procesando" class="alert alert-danger" role="alert">
                            Debes cubrir todos los campos
                        </div>
                        <div v-if="correct" class="alert alert-succes" role="alert">
                            Usuario dado de alta correctamente
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "FormularioUsuario",
    data() {
        return {
            procesando: false,
            correcto: false,
            error: false,
            usuario: {
                name: "",
                email: ""
            }
        }
    },
    methods: {
        enviarFormulario() {
            this.procesando = true;
            this.resetEstado();

            if (this.nameInvalido || this.emailInvalido) {
                this.error = true;
                return;
            }

            this.$emit("crearUsuario", this.usuario);
            this.$refs.name.focus();
            this.error = false;
            this.correcto = true;
            this.procesando = false;

            this.usuario = {
                name: "",
                email: ""
            }
        },
        resetEstado() {
            this.correcto = false;
            this.error = false;
        }
    },
    computed: {
        nameInvalido() {
            return this.usuario.name.length < 1;
        },
        emailInvalido() {
            return this.usuario.email.length < 1;
        }
    }
}
</script>

<style scoped>
    
</style>