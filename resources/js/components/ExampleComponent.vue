<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Laravel Vue Datatables Component Example - ItSolutionStuff.com</div>

                    <div class="card-body">
                        <datatable :columns="columns" :data="rows"></datatable>
                        <datatable-pager v-model="page" type="abbreviated" :per-page="per_page"></datatable-pager>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    import DatatableFactory from 'vuejs-datatable';

    export default {
        components: { DatatableFactory },
        mounted() {
            console.log('Component mounted.')
        },
        data(){
            return {
                columns: [
                        {label: 'id', field: 'id'}, 
                        {label: 'Name', field: 'name'},
                        {label: 'Email', field: 'email'}
                    ],
                rows: [],
                page: 1,
                per_page: 10,
            }
        },
        methods:{
            getUsers: function() {
                axios.get('/users').then(function(response){
                    this.rows = response.data;
                }.bind(this));
            }
        },
        created: function(){
            this.getUsers()
        }
    }
</script>
