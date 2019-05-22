<template>
    <div id="listado" v-cloak>
        <h1 class="text-center text-info">Proyectos</h1>
        <div class="sk-cube-grid" v-if="projects.length === 0">
            <div class="sk-cube sk-cube1"></div>
            <div class="sk-cube sk-cube2"></div>
            <div class="sk-cube sk-cube3"></div>
            <div class="sk-cube sk-cube4"></div>
            <div class="sk-cube sk-cube5"></div>
            <div class="sk-cube sk-cube6"></div>
            <div class="sk-cube sk-cube7"></div>
            <div class="sk-cube sk-cube8"></div>
            <div class="sk-cube sk-cube9"></div>
        </div>
        <div id="ciclo" class="proyecto" v-for="proyecto in projects">
            <div class="card">
                <div class="card-header text-white bg-primary mb-3">
                    <h2 class="text-justify">{{ proyecto.title }}</h2>
                </div>
                <div class="card-body">
                    <p>Descripción: {{ proyecto.description }}</p>
                    <button class="btn btn-danger" v-on:click="deleteProject(proyecto)">Eliminar Proyecto</button>
                </div>
                <div class="card-footer">
                    <p>Actualizado el: {{ proyecto.updated_at | formateDate('DD MM YYYY') }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: "proyectos",
        data() {
            return { projects: [] }
        },
        methods: {
            deleteProject: function(project){
                console.warn("Eliminar el proyecto: ", project);
            },
        },
        filters: {
            formateDate: ( date, outputFormat) =>{//Filtro con arrow functions
                return moment(date).format(outputFormat);
            }
        },
        mounted: function() {//Función en el Ciclo de vida del Vue.js ciclo mounted.
            const serverURL = 'http://172.104.91.187/projects';

            const configAxios= {
                url: serverURL,
                method: 'get', //Metodo de comunicación get, post, delete, put.
                responseType: 'json', // default
                responseEncoding: 'utf8', // default
                // `data` is the data to be sent as the request body
                data: {},
                // `headers` are custom headers to be sent
                headers: {
                    'Content-Type': 'application/json',
                    'Api-Token': 'jJHGtk3IoZ84CmKlDz5N206w46yaj6v4mk0vXdTDl5w80iqnk0skp9Jp6NQ3'
                },
            };
            axios.request(configAxios).then( (response) => {
                console.log(response);//Prueba de comunicación
                this.projects = response.data; //Asigna la respuesta del json a la data del vue
            });
        },
    }
</script>

<style scoped>
    .proyecto{
        color: #222;
    }
    [v-cloak]{
        display: none;
    }
</style>
