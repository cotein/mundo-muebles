<template>
    <li class="sidenav-item has-subnav" :class="{active:'lista_precios' == parent_name, open:'lista_precios' == parent_name}">
        <a href="#" >
            <span class="sidenav-icon icon icon-file-text-o"></span>
            <span class="sidenav-label">Lista de precios</span>
        </a>
        <ul class="sidenav level-2" v-for="(link, index) in links" :key="index">
            <li @click="getPathName(link.name)" :class="{active:path_name == link.name}" > 
                <a :href="link.url">
                    <span class="icon icon-circle-o fa-lg"></span>
                    <span class="sidenav-label">{{link.name}}</span>
                </a>
            </li>
        </ul>
    </li>
</template>

<script>
import collect from 'collect.js';
export default {
    data() {
        return {
            active_li : false,
            open_li : false,
            path_name : false,
            parent_name : false,
            links : [
                {
                    active : false,
                    name : 'Agregar',
                    url : '/empresa/lista-precios/nueva',
                    parent_name : 'lista_precios'
                },
                
            ]
        }
    },
    methods : {
        click_link(url){
            let $vm = this;
            let  links = collect($vm.links);
            $vm.active_li = true;
            links.each((l)=>{
                if (l.url == url) {
                    l.active = true;
                }
            })
        },
        click_open_li(){
            this.open_li = !this.open_li
        },
        getPathName(name){
            sessionStorage.setItem('path_name', name);
            sessionStorage.setItem('parent_name', 'lista_precios');
        }
    },
    mounted(){
        this.path_name = sessionStorage.getItem('path_name');
        this.parent_name = sessionStorage.getItem('parent_name');
    }
}
</script>

<style>

</style>
