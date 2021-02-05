<template>
     <div class="menu">
        <div class="logo">
            <div class="icon-bar"></div>
            <div class="logo-page"></div>
        </div>
        <div class="menu__content">
            <div class="menu__item">
                <div class="menu__icon1"></div>
                <div class="menu__content1">Tong quan</div>
            </div>
            <div class="menu__item">
                <div class="menu__icon2"></div>
                <div class="menu__content1">Bao cao</div>
            </div>
            <div class="menu__item">
                <div class="menu__icon3"></div>
                <div class="menu__content1">Mua hang</div>
            </div>
            <div class="menu__item">
                <div class="menu__icon4"></div>
                <div class="menu__content1">Danh muc khach hang</div>
            </div>
            <div class="menu__item">
                <div class="menu__icon5"></div>
                <div class="menu__content1">Thiet lap he thong</div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Menu'
}
</script>

<style scoped>
    .menu{
        width: 172px;
        margin: 0px;
    }
    .menu .logo{
        position:relative;
        width: 100%;
        height: 60px;   
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
    }

    .menu .logo .icon-bar {
        width: 30px;
        height: 30px;      
        background-image: url('../assets/img/toggle.png');
        background-size: contain;
    }
    .menu .logo .logo-page {
        width: 110px;
        height: 30px;
        background-image: url('../assets/img/cukcuk-logo.png');
        background-size: contain;
    }
    .menu .menu__content{
        position: relative;
        width: 100%;
        margin-top: 30px;
    }
    .menu .menu__content .menu__item {
        display: flex;
        margin-left: 15px;
        height: 80px;
        width: 100%;
        
    }
    .menu .menu__content .menu__item .menu__icon1 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/dashboard.png');
        background-size: contain;
    }
    .menu .menu__content .menu__item .menu__icon2 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/report.png');
        background-size: contain;
    }
    .menu .menu__content .menu__item .menu__icon3 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/dashboard.png');          
        background-size: contain;
    }
    .menu .menu__content .menu__item .menu__icon4 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/dic-employee.png');
        background-size: contain;
    }
    .menu .menu__content .menu__item .menu__icon5 {
        width: 30px;
        height: 30px;
        background-image: url('../assets/icon/setting.png');
        background-size: contain;
    }
    .menu .menu__content .menu__item .menu__content1{
        padding-top: 6px;
        margin-left: 10px;
    }      
</style>