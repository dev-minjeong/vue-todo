<template>
  <div>
    <ul>
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
            <i class="checkBtn fa-solid fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}"
                v-on:click="toggleComplete(todoItem, index)"></i>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
            <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                <i class="fa-solid fa-trash-can"></i>
            </span>
        </li>
    </ul>
  </div>
</template>

<script>
import { ID } from 'webpack/lib/ModuleFilenameHelpers';

export default {
    data: function() {
        return {
            todoItems:[]
        }
    },
    methods: {
        removeTodo: function(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
            
        },
        toggleComplete: function(todoItem, index){
            todoItem.completed = !todoItem.completed;
            // localstorage는 업데이트 기능이 없기 때문에
            // 업데이트 원할 시 삭제 후 추가방식으로 구현해야 함
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem) )
        }
    },
    created: function() { // 뷰 라이프 사이클 - 뷰 인스턴스 생성 후 호출
        if(localStorage.length > 0) {
            for(let i = 0; i < localStorage.length; i++) {
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }// console.log(localStorage.key(i));
            }
        }
    }

}
</script>

<style scoped>
    ul {
        list-style-type: none ;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
        cursor: pointer;
    }
    .checkBtnCompleted {
        color: #b3adad;
    }
    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }
    .removeBtn {
        margin-left: auto;
        color: #de4343;
        cursor: pointer;
    }
</style>