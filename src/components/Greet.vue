<template>
    <div>
        Hello {{name}} aka {{heroName}}
    </div>
</template>

<script>
export default {
    name:"Greet",
    props:['name', 'heroName']
    
}
</script>

<style>
    
</style>