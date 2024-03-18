<template>
    <div>
        Part of Article - {{sectionName}}

        Same part name - {{partName}}
        
    </div>
</template>
<script>
export default {
    // inject runs before data so, you can use injected datas in data properties as initial values as well 
    // for learning aliasing of injected properties, providing default values to them, etc consult provide/inject docs of vue js 
    inject:['sectionName'],
    data(){
        return {
            partName:this.sectionName
        }
    }
    
}
</script>
<style>
    
</style>