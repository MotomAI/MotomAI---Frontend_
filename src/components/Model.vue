<template>
    <div id="app">
        <button class="color_boto boto_config " v-on:click = getGraph() >{{name}}</button>
            <button v-if = click>
                <img v-bind:src="graph" />
                <h4>Based on the tendency of this moto model, the require parts to fix it will be out of stock</h4>
                <h3>Used parts:</h3>
                <table class="center">
                <thead>
                    <tr>
                    <th>#</th>
                    <th>Reference ID</th>
                    <th>Stock</th>
                    <th>Required</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(part,i) in parts" :key="i">
                    <th scope="row"> {{i}} </th>  
                    <td>{{ part.part.id }}</td> 
                    <td>{{ part.part.total_in_stock}}</td>  
                    <td>{{ part.required}}</td>  
                    </tr>
                </tbody>
                </table>
                <h4>One or more parts associated to this model will become out of stock based on the global prediction</h4>

            </button>

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
        },
        "parts": {
            type: Array,
            required: true
        }
    },
    methods: {
        async getGraph() {
        this.click = !this.click
        await axios.get('http://34.134.230.81/graph/' + this.id)
            .then(response => {
            this.graph = 'data:image/png;base64,'+response.data.graph ;
            console.log(this.parts);
            
            console.log(this.graph);
            })
            .catch(e => {
            console.log(e);
            })
        }
    }
}
</script>