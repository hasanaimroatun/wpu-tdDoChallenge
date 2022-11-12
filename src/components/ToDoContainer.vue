<template>
    <div>
        <div class="title">#todo</div>
        <nav class="navbar navbar-expand bg-transparent position-absolute start-50 translate-middle ">
            <div class="container-fluid">
                <ul class="navbar-nav">
                    <li class="nav-item">
                    <a class="nav-link" 
                        href="#" 
                        @click="activeTab = 'AllContent'" 
                        :style="bStyle1"
                    >
                        All
                    </a>
                    </li>
                    <li class="nav-item">
                    <a class="nav-link" 
                        href="#" 
                        @click="activeTab = 'ActiveContent'" 
                        :style="bStyle2"
                    >
                        Active
                    </a>
                    </li>
                    <li class="nav-item">
                    <a class="nav-link" 
                        href="#" 
                        @click="activeTab = 'CompletedContent'" 
                        :style="bStyle3"
                    >
                        Completed
                    </a>
                    </li>
                </ul>
            </div>
        </nav>
        <div class="inputContainer position-absolute start-50 translate-middle">
            <input 
                type="text" 
                class="form-control" 
                placeholder="add details" 
                aria-label="add details" 
                aria-describedby="button-addon"
                v-model="todoData"
            >
            <button 
                class="btn btn-primary" 
                type="button" 
                id="button-addon"
                @click="addTodo"
            >
                Add
            </button>
        </div>
        <keep-alive>
            <component :is='activeTab' class="content"/>
        </keep-alive>
        <div class="createdBy">created by <a href="#">hasanaimroatun</a> - devChallenges.io</div>
    </div>
</template>

<script>
import AllContent from './AllContent.vue'
import ActiveContent from './ActiveContent.vue'
import CompletedContent from './CompletedContent.vue' 

    export default {
        name: 'todo-container',
        components: {
            AllContent,
            ActiveContent,
            CompletedContent,
        },
        data() {
            return {
                activeTab: 'AllContent',
                bStyle1: {
                    borderBottom: ''
                },
                bStyle2: {
                    borderBottom: ''
                },
                bStyle3: {
                    borderBottom: ''
                },
                todoData: '',
                todoContainer: []
            }
        },
        mounted() {
            this.bStyle1.borderBottom = '4px solid #2F80ED',
            this.bStyle2.borderBottom = '4px solid transparent',
            this.bStyle3.borderBottom = '4px solid transparent'
        },
        updated() {
            this.activeTab == 'AllContent' ? this.bStyle1.borderBottom = '4px solid #2F80ED' : this.bStyle1.borderBottom = '4px solid transparent',
            this.activeTab == 'ActiveContent' ? this.bStyle2.borderBottom = '4px solid #2F80ED' : this.bStyle2.borderBottom = '4px solid transparent',
            this.activeTab == 'CompletedContent' ? this.bStyle3.borderBottom = '4px solid #2F80ED' : this.bStyle3.borderBottom = '4px solid transparent'
        },
        methods: {
            addTodo() {
                this.todoContainer.push(this.todoData)
                console.log(this.todoContainer)
            }
        }
    }
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&family=Raleway:wght@700&display=swap');

.title {
    font-family: 'Raleway', sans-serif;
    font-weight: 700;
    font-size: 36px;
    line-height: 42.26px;
    color: #333333;
}

.navbar li {
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
    font-size: 14px;
    line-height: 17.07px;
    color: #333333;
    border-bottom: 1px solid #BDBDBD;
    width: 200px;
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
    margin-top: 131px;
}

.navbar li a {
    width: fit-content;
}

.navbar li a:focus {
    width: fit-content;
}

.inputContainer {
    width: 610px;
    margin-top: 139px;
    display: flex;
    gap: 25px;
}

input {
    width: 476px;
    height: 56px;
    border: 1px solid #BDBDBD;
}

input,
input::placeholder {
    color: #828282;
}

input:focus {
    outline: none;
    box-shadow: none;
}

button {
    width: 109px;
    background-color: #2F80ED;
    border: 1px solid #2F80ED;
    color: white;
}

.content {
    margin-top: 200px;
}

.createdBy {
    font-family: 'Montserrat', sans-serif;
    font-weight: 500;
    font-size: 14px;
    line-height: 17.07;
    width: 100%;
    text-align: center;
    position: relative;
    top: 130px;
    color: #A9A9A9;
}

.createdBy a {
    font-weight: 700;
    color: inherit;
    text-decoration: none;
}

.createdBy a:hover {
    color: #333333;
}

@media screen and (max-width: 995px) {
    .navbar li {
        width: 150px;
    }

    .inputContainer {
        width: 460px;
    }

    input {
        width: 326px;
    }
}

@media screen and (max-width: 600px) {
        .navbar li {
        width: 110px;
    }

    .inputContainer {
        width: 330px;
    }

    .inputContainer {
        gap: 10px;
    }

    input {
        width: 256px;
    }

    button {
        width: 80px;
    }
}
</style>