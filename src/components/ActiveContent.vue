<template>
    <div>
        <div v-for="todo in todoOngoing" :key="todo">
            <div class="form-check d-flex position-relative tList">
                <input class="form-check-input" type="checkbox" id="flexCheckDefault" @click="addDecoration($event)">
                <label class="form-check-label" for="flexCheckDefault">
                    {{todo.data}}
                </label>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Active-content',
        props: ['todoOngoing', 'addDecoration']
    }
</script>

<style scoped>

</style>