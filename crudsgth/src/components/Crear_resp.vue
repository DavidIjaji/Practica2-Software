<template>  
    <div class="container">
        <div class="card">
            <div class="card-header">
                <h2 class="fw-bold">Crear Activo General</h2> 
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="agregarActivo">
                    <div class="form-group">
                        <label for="documento"></label>
                        <input type="text" name="documento" id="documento" class="form-control" required v-model="activo.documento" placeholder="Serial" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el documento del responsable</small>
                    </div>
                    <div class="form-group">
                        <label for="nombre"></label>
                        <input type="text" name="nombre" id="nombre" class="form-control" required v-model="activo.nombre" placeholder="Nombre" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Agregue el nombre del responsable</small>
                    </div>
                    <div class="form-group">
                        <label for="apellido"></label>
                        <input type="text" name="apellido" id="apellido" class="form-control" required v-model="activo.apellido" placeholder="Marca" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el apellido</small>
                    </div>
                    <div class="form-group">
                        <label for="modelo"></label>
                        <input type="text" name="modelo" id="modelo" class="form-control" required v-model="activo.modelo" placeholder="Modelo" aria-describedby="helpId">
                        <small id="helpId" class="text-muted">Ingrese el modelo</small>
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
    methods: {
        agregarActivo(){
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
            fetch('http://localhost:8000/Practica2-Software/?insertar=0',{
                method: 'POST',
                body:JSON.stringify(datosEnviar)
            })
            .then(respuesta=>respuesta.json())
            .then(datosRespuesta=>{
                console.log(datosRespuesta)
                window.location.href='listar'
            })
        }
    }
}
</script>