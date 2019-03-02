<template>
    <div class="panel panel-default">
        <div class="panel-heading">¿En que estas pensando ahora?</div>

        <div class="panel-body">
     

            <form action="" v-on:submit.prevent="newThought()">
                <div class="form-group">
                    <label for="thought">Ahora estoy pensando en: </label>
                    <input v-model="description" type="text" name="thought" class="form-control">
                </div>
                <button type="submit" class="btn btn-primary">Enviar pensamiento</button>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                description: ''
            }
        },
        methods: {
            newThought(){
                const params = {
                    description: this.description
                };
                
                axios.post('/thoughts', params).then((response) => {
                    const thought = response.data;

                    this.$emit('new', thought);//Enviar a otro componente a un evento creado alla
                    this.description = '';
                });
            }
        }
    }
</script>
