<template>
    <div>
    <header class="mui-bar mui-bar-nav">
        <a class="mui-icon  mui-icon-closeempty mui-pull-left" @click.prevent="back($event)"></a>
        <h1 class="mui-title">选择方向</h1>
    </header>
    <div class="mui-content">

        <ul class="mui-table-view">
            <li class="mui-table-view-cell" v-for="item in datas" @click="select(item)" :style="{color:item.color}">{{item.fname}}</li>
        </ul>
    </div>
    </div>
</template>

<script>
    export default {
        name: "select-fangxiang",
        methods:{
            back(e){
                this.$router.go(-1);
            },
            select(item){
                this.datas.forEach(function (item,index) {
                    item.color="#000";
                })
                item.color="blue";
                this.$store.commit("setFname",{fname:item.fname,fid:item.fid})
            }
        },
        data(){
            return {
                datas:[],
                color:"red"
            }
        },
        mounted(){
            fetch("/api/fangxiang/select").then(function (e) {
                return e.json();
            }).then((e)=>{
                e.forEach(function (item,index) {
                    item.color="#000";
                })
                this.datas=e;
            })
        }
    }
</script>

<style scoped>

</style>