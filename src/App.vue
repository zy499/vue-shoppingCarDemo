<template>
    <div id="app">
        <h1 :style="{ textAlign: 'center' }">购物车hhhDdhh</h1>
        <hr />
        <div>
            <h3>添加课程</h3>
            <div>
                <label for="">课程名称：</label>
                <input type="text" v-model="name" />
            </div>
            <div>
                <label for="">课程价格：</label>
                <input type="number" v-model="price" />
            </div>
            <button @click="addCourseList">添加到课程列表</button>
        </div>
        <hr />
        <div>
            <h3>课程列表</h3>
            <table>
                <tr>
                    <th>课程名称</th>
                    <th>课程价格</th>
                    <th>操作</th>
                </tr>
                <tr v-for="(item, index) in courseList" :key="index">
                    <td>
                        {{ item.name }}
                    </td>
                    <td>
                        {{ item.price }}
                    </td>
                    <td>
                        <button @click="addItemCar(index)">添加到购物车</button>
                        <button @click="delItem(index)">删除</button>
                    </td>
                </tr>
            </table>
        </div>
        <hr />
        <car :courseCarList="courseCarList" v-on:removeItem="remove" />
    </div>
</template>

<script>
import Car from "./components/Car.vue";
export default {
    name: "app",
    components: {
        Car
    },
    data() {
        return {
            //添加表单obj
            name: "",
            price: "",
            //课程列表list
            courseList: [
                {
                    id: 1,
                    name: "web全栈",
                    price: "9888"
                },
                {
                    id: 2,
                    name: "java",
                    price: "8889"
                }
            ],
            //向购物车组件传递的list
            courseCarList: []
        };
    },
    methods: {
        //添加课程
        addCourseList() {
            if(!this.name){
                alert('请输入课程名称!') 
                return
            }
            if(!this.price){
                alert('请输入课程价格!')
                return
            }
            this.courseList.push({
                name: this.name,
                price: this.price,
            });
            this.name = "";
            this.price = "";
        },
        //删除课程
        delItem(index) {
            this.courseList.splice(index, 1);
        },
        //添加到购物车
        addItemCar(index) {
            let obj = this.courseList[index];
            let isHasCourse = this.courseCarList.find(
                item => item.id === obj.id
            );
            if (isHasCourse) {
                isHasCourse.number += 1;
            } else {
                this.courseCarList.push({
                    ...obj,
                    number: 1,
                    isActive: true
                });
            }
        },
        //删除购物车商品
        remove(index) {
            this.courseCarList.splice(index, 1);
        }
    }
};
</script>
<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
