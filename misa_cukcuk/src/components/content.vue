<template>
    <div class="content">
        <div class="division1">
            <div class="info"><strong>Danh sách nhân viên</strong></div>
            <div class="add">
                <div class="content__icon1"> </div>
                <div class="adding_new_employee" v-on:click = "$emit('openDialog')">
                    Thêm nhân viên
                </div>
            </div>
        </div>

        <div class="division2">
            <div class="finding">
                <span class="content__icon2"></span>
                <input type="text" placeholder="Tim kiem theo ma, Ten khach hang" style="border: 0px solid;width:270px; height: 25px;" />
            </div>
            <div class="em_category">
                <select id="category" style=" height:32px;"
                @change="CateOnChange" v-model="selectedCatId" >
                    <option value="0">Tất cả phòng ban</option>
                    <option value="1">Phòng marketing</option>
                    <option value="2">Phòng nhân sự</option>
                    <option value="3">Phòng công nghệ</option>
                </select>
            </div>
            <div class="em_postiton">
                <select id="position" style=" height:32px;" @change = "PosOnChange" v-model="selectedPosId" >
                    <option value="0">Tất cả vị trí</option>
                    <option value="1">Giám đốc </option>
                    <option value="2">Nhân viên marketing</option>
                    <option value="3">Thu ngân</option>
                </select>
            </div>
            <div class="content__icon3"></div>
        </div>

        <div class="division3">
            <table id="employee">
                <thead>
                    <tr>
                        <th class="employee_code">Mã nhân viên</th>
                        <th class="fullName">Họ và tên</th>
                        <th class="gender">Giới tính</th>
                        <th class="date__of__birth">Ngày sinh</th>
                        <th class="phone_num">Điện thoại</th>
                        <th class="email">Email</th>
                        <th class="emRole">Chức vụ</th> 
                        <th class="address">Phòng ban</th>
                        <th>Mức lương cơ bản</th>
                        <th>Tình trạng công việc</th>
                    </tr>
                </thead>
                <tbody>
                    <tr :key="listData.id" v-for="listData in listSlicedData"
                    @dblclick="$emit('emitCusInfo', listData.EmployeeId)" 
                    class="hoverEm"
                    >
                        <td>{{listData.EmployeeCode}}</td>
                        <td>{{listData.FullName}}</td>
                        <td>{{listData.Gender | changingGender}}</td>
                        <td>{{listData.DateOfBirth | changingDate }}</td>
                        <td>{{listData.PhoneNumber}}</td>
                        <td>{{listData.Email}}</td>
                        <td>{{listData.Position}}</td>
                        <td>{{listData.Category}}</td>
                        <td>{{listData.BaseSalary}}</td>
                        <td>{{listData.WorkStatus}}</td>
                    </tr>     
                </tbody>
            </table>
        </div>
        <Footer v-on:openPageNum = "openPageNum" />
    </div>
</template>
<script>
import Footer from './footer';
import moment from 'moment';
// import axios from 'axios';

export default {
    name:'Content',
    components: {
        Footer,
    },
    computed:{
        listSlicedData(){
            return this.listDatas.slice(125*(this.currentPage-1), 125*this.currentPage)
        }
    },
    props:["listDatas"],
    methods: {
        CateOnChange(){
            if (this.selectedCatId  == 0){
                this.selectedCatContent = "phòng"
            }
            if (this.selectedCatId  == 1){
                this.selectedCatContent = "phòng marketing "
            }
            else if (this.selectedCatId  == 2){
                this.selectedCatContent = "phòng nhân sự "
            }
             else if (this.selectedCatId  == 3){
                this.selectedCatContent = "phòng công nghệ "
            }
            this.$emit('sortByCate', this.selectedCatContent);
        },
        openPageNum(param){
            console.log("pr:" + param);
            this.currentPage = param;
            // console.log(this.listSlicedData);
        },
        PosOnChange(){
            console.log(this.selectedPosId);
            if (this.selectedPosId  == 0){
                this.selectedPosContent = " "
            }
            if (this.selectedPosId  == 1){
                this.selectedPosContent = "giám đốc"
            }
            else if (this.selectedPosId  == 2){
                this.selectedPosContent = "nhân viên marketing "
            }
             else if (this.selectedPosId  == 3){
                this.selectedPosContent = "thu ngân "
            }
            this.$emit('sortByPos', this.selectedPosContent);
        }
    },
    data() {
        return {
            selectedCatContent:"",
            selectedCatId:"0",
            selectedPosContent:"",
            selectedPosId:"0",
            currentPage: 1,
        }
    },
    filters: {
        changingGender(value){
            if (value == 0 ){
                return "Nữ";
            }
            else{
                return "Nam";
            }
        },
        changingDate(date){
            if (!date)
                return "";
            else
                return moment(date).format('DD-MM-YYYY');
        }
    }
}

</script>

<style scoped>
    .content {
        position: absolute;
        top: 60px;
        left: 200px;
        bottom: 0px;
        right: 0px;
        border-left: 1px solid #9e9e9ecf;
        border-top: 1px solid #9e9e9ecf;
    }
    .hoverEm:hover {
        background-color: aqua;
        cursor: pointer;
    }
    .division1{
        margin-top: 40px;
        display: inline-flex;
    }
    .division1 .info{
        font-size: 40px;
        padding-left: 40px;
    }
    .division1 .add {
        width: 150px;
        height: 30px;
        background-color: #4caf50fa;    
        margin-left: 700px;
        border-radius: 2px;
        display: inline-flex;
    }
    .division1 .add .pop_up_window{
        width: 200px;
        height: 200px;
        position: absolute;
        background-color: blue;
        visibility: hidden;
    }
    .division1 .add .content__icon1 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/add.png');
        background-size: contain;
    }
    .division1 .add .function{
        padding-top:5px;
    }
     .division1 .add .adding_new_employee {
            padding-top: 5px;
    }
    .division1 .add:hover{
        cursor: pointer;
        background: rgb(194, 166, 8);
    }
    .division2 {
        height: 100px;
        display: inline-flex;
    }
    .division2 .finding {
        width: 300px;
        height: 30px;
        display: inline-flex;
        margin-top: 30px;
        margin-left: 40px;
        align-items: center;
        justify-content: center;
        border: 1px solid black;
        border-radius: 2px;
        color: darkgrey;
    }
    .division2 .finding .content__icon2 {
        width: 20px;
        height: 20px;
        background-image: url('../assets/icon/search.png');
        background-size: contain;
    }
    .division2 .content__icon3 {         
        margin-left: 500px;
        margin-top: 30px;
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/refresh.png');          
        background-size: contain;
        border: 1px solid black;
        border-radius: 2px;  
    }
    .division3 {
        height: 55vh;
    }
    table {
        Overflow-x:scroll;
        Overflow-y:scroll; 
        width: 1300px;
        border-collapse: collapse;
        border-top: 1px solid darkgray;
    }
    .division3 {
        Overflow-x: scroll;
        Overflow-y: scroll;
    }
    th, td{
        text-align: left; 
        padding-left: 20px;
        border-top: 1px solid darkgray;       
    }
    thead tr {
        background-color:#9e9e9e78;
    }
    tbody tr:nth-child(even) { 
        background-color: #9e9e9e47; 
    } 
     .division2 .em_category {
        margin-top: 30px;
        margin-left: 30px;
    }
    .division2 .em_postiton {
        margin-top: 30px;
        margin-left: 30px;
    }
</style>