<!--  -->
import { match } from 'minimatch';
<template>
    <div class="">
        <h3>购物车</h3>
        <hr />
        <table>
            <tr>
                <th>勾选</th>
                <th>名称</th>
                <th>价格</th>
                <th>数量</th>
                <th>总价</th>
            </tr>
            <tr v-for="(item, index) in courseCarList" :key="index">
                <td>
                    <input type="checkbox" v-model="item.isActive" />
                </td>
                <td>
                    {{ item.name }}
                </td>
                <td>
                    {{ item.price }}
                </td>
                <td>
                    <button @click="minus(index)">-</button>
                    {{ item.number }}
                    <button @click="add(index)">+</button>
                </td>
                <td>
                    {{ item.price * item.number }}
                </td>
            </tr>
            <tr>
                <td></td>
                <td colspan="2">
                    总数量:{{ isActiveCourse }}/{{ allCourseList }}
                </td>
                <td colspan="2">总价:{{ allCoursePrice }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
    props: ["courseCarList"],
    //import引入的组件需要注入到对象中才能使用
    components: {},
    data() {
        //这里存放数据
        return {};
    },
    //监听属性 类似于data概念
    computed: {
        isActiveCourse() {
            return this.courseCarList.filter(item => item.isActive).length;
        },
        allCourseList() {
            return this.courseCarList.length;
        },
        allCoursePrice() {
            let num = 0;
            this.courseCarList.forEach(item => {
                if (item.isActive) {
                    num += item.price * item.number;
                }
            });
            return num;
        }
    },
    //监控data中的数据变化
    watch: {},
    //方法集合
    methods: {
        minus(index) {
            let num = this.courseCarList[index].number;
            if (num > 1) {
                this.courseCarList[index].number -= 1;
            } else {
                if (window.confirm("您确定要删除此商品吗?")) {
                    this.$emit("removeItem", index);
                    //注意$emit子组件向父组件传参后父组件在v-on绑定事件函数不需要再传值 否则vue会警告参数没有在data数据集里定义
                }
            }
        },
        add(index) {
            this.courseCarList[index].number += 1;
        }
    },
    //生命周期 - 创建完成（可以访问当前this实例）
    created() {},
    //生命周期 - 挂载完成（可以访问DOM元素）
    mounted() {},
    beforeCreate() {}, //生命周期 - 创建之前
    beforeMount() {}, //生命周期 - 挂载之前
    beforeUpdate() {}, //生命周期 - 更新之前
    updated() {}, //生命周期 - 更新之后
    beforeDestroy() {}, //生命周期 - 销毁之前
    destroyed() {}, //生命周期 - 销毁完成
    activated() {} //如果页面有keep-alive缓存功能，这个函数会触发
};
</script>
<style lang="" scoped></style>
