<template>
    <div id="app">
        <button class="color_boto boto_config " v-on:click = getGraph() >{{name}}</button>
            <button v-if = click>
            </button>
            <img v-bind:src="'data:image/jpg;base64,'+graph" />

    </div>
</template>

<script>
import axios from 'axios'

export default {
    name : "model-button",
    data() {
        return {
            click: false,
            graph: '',

        }
    },
    props: {
        "name": {
            type: String,
            required: true
        },
        "warn": {
            type: Boolean,
            required: false
        },
        "id": {
            type: Number,
            required: true
        }
    },
    methods: {
        async getGraph() {
        this.click = !this.click
        await axios.get('http://34.134.230.81/graph/' + this.id)
            .then(response => {
            this.graph = response.data.graph ;
            
            console.log(this.graph);
            })
            .catch(e => {
            console.log(e);
            })
        }
    }
}
</script>