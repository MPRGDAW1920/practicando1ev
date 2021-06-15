<template>
    <div id="app">
        <h1 class="text-center mb-2">Buscar usuario de GitHub</h1>

        <!-- TODO: Añadir título de la página y nombre de autor -->
		<h3 class="text-center">Examen Diseño Interfaces: Repositorio GitHub</h3>
		<h3 class="text-center">                   Autor: MP Rodes</h3>

        <!-- TODO: Crear campo de texto para buscar el usuario -->
		<div class="container-fluid">
			<input type="text" class="form-control" v-model="user" @keydown.enter="obtenerRepositorios" placeholder="Introducir nombre Usuario">
		</div>

        <!-- TODO: Crear componente de alerta de error -->
		<div class="container-fluid">
			<div v-if="isError" class="alert alert-danger" role="alert">
				Error usuario no es correcto
			</div>
		</div>

        <!-- TODO: Crear lista de repositorios llamando al componente GitHubRepo -->
		<div class="d-inline-flex col-4 m-0 p-o" v-for="i in repositorios" :key="i.id">
			<GitHubRepo v-if="!isError" :repo="i"> </GitHubRepo>
		</div>
    </div>
</template>

<script>
// Importar librería 'axios' para llamadas AJAX
import axios from 'axios';

// TODO: Importar componente GitHubRepo
import GitHubRepo from './components/GitHubRepo.vue'

export default {
    name: 'App',
    components: {
        // TODO: Añadir componente GitHubRepo
		GitHubRepo
    },
    data: function() {
        return {
            user: '',
            repositorios: [],
            // TODO: Añadir variables auxiliares para mostrar/ocultar datos y/o errores
			userData: {},
            isError : false,
            disabled: false,
            showRepos: false,
            validUser: false
        }
    },
    methods: {
        obtenerRepositorios: function() {
            // Función para obtener los repositorios del usuario desde la API de GítHub
            // Crear URL del repositorio
            var url = `https://api.github.com/users/${this.user}/repos`;

            // Obtener datos de autenticación de usuario para hacer peticiones
            // autenticadas a la API de GitHub
            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";

            // Lanzar petición AJAX con Axios
            axios
                .get(url, {
                    auth: {
                        username: userAuth,
                        password: passAuth
                    }
                })
                .then(response => {
                    // La petición es válida. Almacenamos los datos de la respuesta en la variable local 'repositorios'
                    this.repositorios = response.data;

                    // TODO: Añadir funcionalidad para mostrar datos y/o ocultar error
					this.userData = response.data;
                    this.validUser = true;
                    this.isError = false;
                })
                .catch(error => {
                    // La petición no es válida. Indicar que no se han cargado correctamente los repositorios
                    error;

                    // TODO: Añadir funcionalidad para mostrar datos y/o ocultar error
					this.validUser = false;
					this.isError = true;
                })
        }
    }
}
</script>

<style>
</style>
