<template>
     <div class="row">
        <div class="col-log-8 offset-lg-2">
            <div class="table-responsive">
                <DataTable :data= "clientes" :columns="columns" 
                class="table table-striped table-bordered display"
                :options="{responsive:true, autoWidth:false, dom: 'Bfrtip',
                            language:{
                                search:'Buscar', zeroRecords:'No hay registros',
                                info:'Mostrando del _START_a_END_de_TOTAL_registros',
                                infoFiltered:'(Filtrados de _MAX_ registros)',
                                paginate:{first:'Primero', previous:'Anterior', next:'siguiente', last:'Ultimo'}
                            }}">
                    <thead>
                        <tr>
                            <th>Id</th>
                            <th>NOMBRE</th>
                            <th>DIRECCION</th>
                            <th>TELEFONO</th>

                        </tr>
                    </thead>
                </DataTable>


            </div>
        </div>
  </div>
</template>

<script>
    import axios from "axios";
    import DataTable from "datatables.net-vue3";
    import DataTableLib from "datatables.net-bs5";
    import Buttons from "datatables.net-buttons-bs5";
    import ButtonsHtml5 from "datatables.net-buttons/js/buttons.html5";
    import print from "datatables.net-buttons/js/buttons.print";
    import pdfmake from "pdfmake";
    import pdfFont from "pdfmake/build/vfs_fonts";
    import "datatables.net-responsive-bs5";
    import JsZip from "jszip";
    window.JsZip = JsZip;
    DataTable.use(DataTableLib);
    DataTable.use(pdfmake);
    DataTable.use(ButtonsHtml5);
    export default{
        components:{DataTable},
        data(){
            return{
                clientes:null,
                columns:[
                    {data:null, render: function(data, tyte, row, meta)
                        { return `${meta.row+1}`}},
                        {data:"id"},
                        {data:"nombre"},
                        {data:"direccion"},
                        {data:"telefono"}

                ]
            }
        },
        mounted(){
            this.getClientes();
        },
        methods:{
            getClientes(){
                axios.get("https://nyg.onrender.com/api/project/")
                .then((response)=>{
                    console.log(response.data)
                    this.clientes = response.data
                })
                
            }
        }

    }

</script>

