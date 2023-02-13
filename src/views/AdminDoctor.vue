<script setup>
    import Logout from '../components/LogoutNav.vue'
</script>

<template>
    <Logout/>
    <div class="addr">
        <h1> Doctor's Profiles</h1>
    </div>
    <div class="addr1">
        <div class="dp">
            <table cellspacing="0" cellpadding="0" border="0" width="365">
                <tr>
                    <td>
                    <table class="x" cellspacing="0" cellpadding="1" border="1" width="465" >
                        <tr style="color:white;background-color:grey">
                            <th style="width:20.56%">NAME</th>
                            <th style="width:26%">SPECILIZATION</th>
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
                        <tr v-for="dr in drlist" v-bind:key="dr._id" > 
                             <td style="width:30%">{{ dr.firstName+" "+dr.lastName }}</td>
                            <td style="width:38%">{{ dr.spec }}</td>
                            <td style="width:48%">{{ dr.email }}</td>
                            <td style="width:48%">{{ dr.phone }}</td>
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
        name:"admindoctor",
        data(){
            return{
                drlist: ""
            };
        },
        mounted(){
            this.getdr();
        },
        methods:{
            async getdr(){
                try{
                     console.log("yes.. here");
                        let drs = await axios.get(import.meta.env.VITE_APIURL+'/admin/profile/doctor')
                                              .then((res)=>{
                                                this.drlist = res.data;
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
    .addr{
        text-align: center;
        font-size: 10px;
        color: white;
        padding: 10px;
        display: flex;
        /* align-items: center; */
        justify-content: center;
        height: 100%;
        width:100%;
        background-color:black;
        /* float: left; */
    }
    /* .addr2{
        height: 500px;
        width: 100%;
        background-color: bisque;
    } */
    .dp{
        color: #000;
        background-color: burlywood;
        margin-top : 50px;
        /* margin-right: -5px; */
        margin-left: 125px;
        height: 250px;
        width: 660px;
    }
    .x {
            margin-left: 1px;
            width: 660px;
            /* font-size: 20px;
            height: 100%;
            table-layout: fixed; */
    }
    td{
        text-align: center;
    }
</style>