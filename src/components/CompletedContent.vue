<template>
    <div>
        Completed Content
        <div v-for="todo in todoCompleted" :key="todo">
            <div class="form-check d-flex position-relative tList">
                <input class="form-check-input" type="checkbox" id="flexCheckDefault" checked>
                <label class="form-check-label text-decoration-line-through labelList" for="flexCheckDefault">
                    {{todo.data}}
                </label>
                <span 
                    class="position-absolute top-50 end-0 translate-middle-y"  
                    @click="delList($event)"
                >
                    <i class="fa-regular fa-trash-can iconDelete"></i>
                </span>
            </div>
        </div>
        <div v-show="todoCompleted.length !== 0">
            <button 
                type="button" 
                class="btn btn-danger mt-4 bDeleteAll" 
                :style="{width: 'fit-content', marginLeft: '500px'}"
                @click="delAllList()"
            >
                <font-awesome-icon icon="fa-regular fa-trash-can" class="me-2"/>
                <span>Delete All</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Completed-content',
        props: ['todoCompleted', 'delList', 'delAllList'],
        data() {
            return {
                
            }
        }
    }
</script>

<style scoped>

</style>