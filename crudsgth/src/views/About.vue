<template>
    <div class="container">

        <div class="card">
            <div class="card-header">
                Activos
            </div>
            <div class="card-body">
                <table class="table">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Marca</th>
                            <th>Modelo</th>
                            <th>Serial</th>
                            <th>CC_Responsable</th>
                            <th>Responsable</th>
                            <th>Area</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="activo in activos" v-bind:key="activo.id">
                            <td>{{activo.id}}</td>
                            <td>{{activo.nombre}}</td>
                            <td>{{activo.marca}}</td>
                            <td>{{activo.modelo}}</td>
                            <td>{{activo.serial}}</td>
                            <td>{{activo.doc_resp}}</td>
                            <td>{{activo.nom_resp}}</td>
                            <td>{{activo.area}}</td>
                            <td>
                                <div class="btn-group" role="group" aria-label="">
                                    <router-link :to="{name:'Home' , params:{id: activo.id} }" class="btn btn-success" >Editar</router-link>
                                    <button type="button" v-on:click="borrarActivo(activo.id)" class="btn btn-danger">Borrar</button>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {

    data(){
        return {
            activos:[]
        }
        
        },

    created: function(){
        this.consultarActivos();

    },
    methods: {
        consultarActivos(){
            fetch('http://localhost:8000/Practica2-Software/?area=0')
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta=>{
                console.log(datosRespuesta)
                this.activos=[]
                if(typeof datosRespuesta.success === 'undefined'){
                    this.activos = datosRespuesta
                }
            }
            ))
            .catch(console.log)
        }
        // borrarActivo(id){
        //     console.log(id);
        //     fetch('http://localhost/pacientes/?borrar='+id)
        //     .then(respuesta=>respuesta.json())
        //     .then((datosRespuesta=>{
        //         console.log(datosRespuesta)
        //         window.location.href='listar'
        //     }
        //     ))
        //     .catch(console.log)

        // }
    }
}
</script>
