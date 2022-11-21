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
                class="form-control tInput" 
                placeholder="add details" 
                aria-label="add details" 
                aria-describedby="button-addon"
                v-model="todoData"
                @keyup.enter="addTodo"
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
            <component :is='activeTab' class="content" 
                :todoContainer='todoContainer'
                :todoAll='todoAll'
                :todoOngoing='todoOngoing' 
                :todoCompleted='todoCompleted'
                :addDecoration='addDecoration'
                :delList='delList'
                :delAllList='delAllList'
            />
        </keep-alive>

        <div v-show="activeTab === 'AllContent'">
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

        <div class="createdBy">created by <a href="https://github.com/hasanaimroatun/wpu-tdDoChallenge">hasanaimroatun</a> - devChallenges.io</div>
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
            let getData = JSON.parse(localStorage.getItem('dataTodo'))     
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
                todoContainer: [],
                todoAll: [],
                todoOngoing: [],
                todoCompleted: [],
                withDecoration: 'text-decoration-line-through',
                displaySetting: 'd-none',
                getData,
            }
        },
        mounted() {
            this.bStyle1.borderBottom = '4px solid #2F80ED',
            this.bStyle2.borderBottom = '4px solid transparent',
            this.bStyle3.borderBottom = '4px solid transparent',

            document.getElementsByClassName('tInput')[0].focus()

            this.getData == null ? this.todoContainer = [] : this.todoContainer = this.getData  
            this.addFilter()          
        },
        updated() {
            this.activeTab == 'AllContent' ? this.bStyle1.borderBottom = '4px solid #2F80ED' : this.bStyle1.borderBottom = '4px solid transparent',
            this.activeTab == 'ActiveContent' ? this.bStyle2.borderBottom = '4px solid #2F80ED' : this.bStyle2.borderBottom = '4px solid transparent',
            this.activeTab == 'CompletedContent' ? this.bStyle3.borderBottom = '4px solid #2F80ED' : this.bStyle3.borderBottom = '4px solid transparent'

        },
        methods: {
            saveToLocal() {
                localStorage.setItem('dataTodo', JSON.stringify(this.todoAll))
            },
            addFilter() {
                this.todoAll = this.todoContainer.filter(t => {
                    return t.status !== 'deleted'
                })

                this.todoCompleted = this.todoAll.filter(t => {
                    return t.status == 'completed'
                })

                this.todoOngoing = this.todoAll.filter(t => {
                    return t.status == 'ongoing'
                })
            },
            addTodo() {
                let fObj = this.todoAll[this.todoAll.findIndex(x => x.data == this.todoData)]
                if(fObj == undefined) {
                    this.todoContainer.push({data:this.todoData, status:'ongoing'})
                } else {
                    alert('Your list already added!')
                }
                
                this.addFilter()
                this.saveToLocal()
            },
            addDecoration(e) {
                e.target.nextSibling.classList.toggle(this.withDecoration)

                let string = e.target.nextSibling.innerHTML
                let findObj = this.todoContainer[this.todoContainer.findIndex(x => x.data == string)]

                setTimeout(() => {
                    if(e.target.nextSibling.classList.contains(this.withDecoration)) {
                        findObj.status = 'completed'
                    } else {
                        findObj.status = 'ongoing'
                    } 

                    this.addFilter()
                    this.saveToLocal()
                    
                    let string = e.target.nextSibling.innerHTML
                    let findObjct = this.todoAll[this.todoAll.findIndex(x => x.data == string)]

                    let lList = document.getElementsByClassName('labelListAll')[this.todoAll.findIndex(x => x.data == string)]
                    let checkList = document.getElementsByClassName('inputListAll')[this.todoAll.findIndex(x => x.data == string)]
                    
                    if(findObjct.status == 'completed') {
                        lList.classList.add(this.withDecoration)
                        checkList.checked = true
                    }
                }, 1000);

            },
            delList(e) {
                let string = e.currentTarget.previousSibling.textContent
                let findObject = this.todoContainer[this.todoContainer.findIndex(x => x.data == string)]
                findObject.status = 'deleted'

                this.addFilter()
                this.saveToLocal()
            },
            delAllList() {
                const listCompleted = document.getElementsByClassName('labelList')

                for(const l of listCompleted) {
                    let findObj = this.todoContainer[this.todoContainer.findIndex(x => x.data == l.textContent)]
                    findObj.status = 'deleted'
                }
                
                this.addFilter()
                this.saveToLocal()
            },
    
        }
    }
</script>

<style>
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

.tInput {
    width: 476px;
    height: 56px;
    border: 1px solid #BDBDBD;
}

.tInput,
.tInput::placeholder {
    color: #828282;
}

.inputContainer input:focus,
.tList input:focus {
    outline: none;
    box-shadow: none;
}

button {
    width: 109px;
    background-color: #2F80ED;
    border: 1px solid #2F80ED;
    color: white;
}

.tList {
    gap: 10px;
    width: 610px;
    margin: 15px auto;
    font-family: 'Montserrat', sans-serif;
    font-weight: 500;
    font-size: 18px;
    color: #000000;
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

    .inputContainer,
    .tList {
        width: 460px;
    }

    .tInput {
        width: 326px;
    }
}

@media screen and (max-width: 600px) {
    .navbar li {
        width: 110px;
    }

    .inputContainer,
    .tList {
        width: 330px;
    }

    .inputContainer {
        gap: 10px;
    }

    .tInput {
        width: 256px;
    }

    button {
        width: 80px;
    }

}
</style>