<template>
    <div>
        All Content
        <div v-for="todo in todoAll" :key="todo">
            <div class="form-check d-flex position-relative tList">
                <input class="form-check-input inputListAll" 
                    type="checkbox" 
                    id="flexCheckDefault" 
                    @click="addDecoration($event)"
                >
                <label 
                    class="form-check-label labelListAll" 
                    for="flexCheckDefault"
                >
                    {{todo.data}}
                </label>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'All-content', 
        props: ['todoAll', 'addDecoration']
    }
</script>

<style scoped>

</style>