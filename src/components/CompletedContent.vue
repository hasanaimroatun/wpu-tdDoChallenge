<template>
    <div>
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
                    <i class="fa-regular fa-trash-can iconDelete" :style="{color: '#bdbdbd'}"></i>
                </span>
            </div>
        </div>
        <div v-show="todoCompleted.length !== 0">
            <div  class="position-absolute start-50 translate-middle mt-4 d-flex justify-content-end completeContentContainer">
                <button 
                    type="button" 
                    class="btn btn-danger mt-4 bDeleteAll" 
                    :style="{width: 'fit-content'}"
                    @click="delAllList()"
                >
                    <font-awesome-icon icon="fa-regular fa-trash-can" class="me-2"/>
                    <span>Delete All</span>
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Completed-content',
        props: ['todoCompleted', 'delList', 'delAllList']
    }
</script>

<style scoped>
.completeContentContainer {
    width: 610px;
}

button span {
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
    font-size: 12px;
    line-height: 14.63px;
}

@media screen and (max-width: 995px) {
    .completeContentContainer {
        width: 460px;
    }
}

@media screen and (max-width: 600px) {
    .completeContentContainer {
        width: 330px;
    }
}
</style>