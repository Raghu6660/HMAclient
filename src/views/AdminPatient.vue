<script setup>
    import { RouterLink, RouterView } from 'vue-router'
    import Logout from '../components/LogoutNav.vue'
</script>

<template>
    <Logout/>
    <div class="addr">
        <h1> Patients's Profiles</h1>
    </div>
    <div class="addr1">
        <div class="dp">
            <table cellspacing="0" cellpadding="0" border="0" width="365">
                <tr>
                    <td>
                    <table class="x" cellspacing="0" cellpadding="1" border="1" width="465" >
                        <tr style="color:white;background-color:grey">
                            <th style="width:20.56%">NAME</th>
                            <th style="width:26%">SYMPTOMS</th>
                            <th style="width:24%">EMAIL</th>
                            <th style="width:8%">MOBILE</th>
                        </tr>
                    </table>
                    </td>
                </tr>
                <tr>
                    <td>
                    <div style="width:975px; height:159px; overflow:auto;">
                        <table class="x" cellspacing="0" cellpadding="1" border="1" width="345" >
                        <tr v-for="pa in palist" v-bind:key="pa._id" > 
                             <td style="width:30%">{{ pa.firstName+" "+pa.lastName }}</td>
                            <td style="width:38%">{{ pa.symptoms }}</td>
                            <td style="width:48%">{{ pa.email }}</td>
                            <td style="width:48%">{{ pa.phone }}</td>
                        </tr>
                        </table>  
                    </div>
                    </td>
                </tr>
            </table>
            </div>
    </div>
</template>


<script>
     import axios from 'axios';
     import { onMounted } from 'vue';
    export default{
        name:"adminpatient",
        data(){
            return{
                palist: ""
            };
        },
        mounted(){
            this.getpa();
        },
        methods:{
            async getpa(){
                try{
                        let pas = await axios.get(import.meta.env.VITE_APIURL+'/admin/profile/patient')
                                              .then((res)=>{
                                                this.palist = res.data;
                                              })
                                              .catch((err)=>{
                                                console.log(err);
                                              })
                }
                catch(err){
                    console.log(err);
                }
            }
        }
    }
</script>




<style>
    .logout{
        height: 38px;
    }
    .llog{
        color: rgb(210, 92, 214);
        float: right;
        margin-top: 5px;
        border-style: groove;
        border-radius: 10px;
        background-color: rgb(221, 234, 78);
    }
</style>