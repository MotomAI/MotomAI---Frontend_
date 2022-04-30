<template>
    <div id="app">  
        <meta content ="width=device-width, initial-scale=1.0" name="viewport">
        <h1 class= "title">{{titol}}</h1>
  </div>
</template>

<script>

export default {
    name : "titol-panel",
    data() {
        return {
            titol: 'Panel de control'
        }
    }
}
</script>