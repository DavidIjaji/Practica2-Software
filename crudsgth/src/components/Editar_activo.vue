<template>  
    <div class="container">

        <div class="card">
            <div class="card-header">
                <h2 class="fw-bold">Editar Activo Existente</h2> 
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="actualizarActivo">
                    <div class="form-group">
                        <label for="nombre"></label>
                        <input type="text" name="nombre" id="nombre" class="form-control" required v-model="activo.nombre" placeholder="Nombre" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Agregue el nombre</small>
                    </div>
                    <div class="form-group">
                        <label for="marca"></label>
                        <input type="text" name="marca" id="marca" class="form-control" required v-model="activo.marca" placeholder="Marca" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese la marca</small>
                    </div>
                    <div class="form-group">
                        <label for="modelo"></label>
                        <input type="text" name="modelo" id="modelo" class="form-control" required v-model="activo.modelo" placeholder="Modelo" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el modelo</small>
                    </div>
                    <div class="form-group">
                        <label for="serial"></label>
                        <input type="text" name="serial" id="serial" class="form-control" required v-model="activo.serial" placeholder="Serial" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el código serial</small>
                    </div>
                    <div class="form-group">
                        <label for="doc_resp"></label>
                        <input type="text" name="doc_resp" id="doc_resp" class="form-control" required v-model="activo.doc_resp" placeholder="Documento del responsable" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el documento del responsable</small>
                    </div>
                    <div class="form-group">
                        <label for="nom_resp"></label>
                        <input type="text" name="nom_resp" id="nom_resp" class="form-control" required v-model="activo.nom_resp" placeholder="Nombre del responsable" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el nombre completo del responsable</small>
                    </div>
                    <div class="form-group">
                        <label for="area"></label>
                        <input type="text" name="area" id="area" class="form-control" required v-model="activo.area" placeholder="Área" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el área al cual pertenece el activo</small>
                    </div>
                    <div class="btn-group" role="group" aria-label="">
                        <button type="submit" class="btn btn-success">Guardar</button>
                        <router-link :to="{name:'Listar'}" class="btn btn-danger">Cancelar</router-link>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            activo: {}
        }
    },
    created: function() {
        this.obtenerActivo();
    },
    methods: {
        actualizarActivo(){
            console.log(this.activo)
            let datosEnviar = {
                id: this.activo.id,
                nombre: this.activo.nombre,
                marca: this.activo.marca,
                modelo: this.activo.modelo,
                serial: this.activo.serial,
                doc_resp: this.activo.doc_resp,
                nom_resp: this.activo.nom_resp,
                area: this.activo.area
            }
            fetch('http://localhost:8000/Practica2-Software/?t=0&actualizar='+this.$route.params.id,{
                method: 'POST',
                body:JSON.stringify(datosEnviar)
            })
            .then(respuesta=>respuesta.json())
            .then(datosRespuesta=>{
                console.log(datosRespuesta)
                window.location.href='listar'
            })
        },
        obtenerActivo(){
            console.log(this.$route.params.id)
            fetch('http://localhost:8000/Practica2-Software/?t=0&consultar='+this.$route.params.id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta=>{
                console.log(datosRespuesta[0])
                this.activo = datosRespuesta[0]
            }))
            .catch(console.log)
        }
    }
}
</script>