<template>
    <div id="app">  
        <ul class = info>
            <img v-bind:src="'data:image/jpg;base64,'+imageBytes" />
        </ul>
  </div>
</template>

<script>

export default {
    name : "graph-image",
    props: {
        "name": {
            type: String,
            required: true
        },
        "imageBytes": {
            type: String,
            required: true
        }
    }
}
</script>
