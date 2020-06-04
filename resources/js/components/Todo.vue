<template>
    <div>
        <input type="text" v-model="name">
        <button @click="posting()">add</button>



        <table v-if="names.length>0">
            <tr>
                <td>id</td>
                <td>name</td>
                <td>status</td>
            </tr>
            <tr v-for="name in names">
                <td>{{name.id}}</td>
                <td>{{name.name}}</td>
                <td>{{name.completed}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: "Todo",
        data:()=>({
            name:'',
            names:[],
        }),
        created(){
            this.getData()
        },
        methods: {
            getData(){
                axios.get('/todo').then(res=>{
                    if(res.status===200)
                        this.names=res.data
                })
            },
            posting() {
                axios.post('/todo', {name:this.name})
                    .then(res => {
                        if(res.status===201){
                            this.names.push(res.data)
                            this.name=''
                        }
                    })
                    .catch(err => {

                    })

            }
        }
    }
</script>

<style scoped>

</style>
