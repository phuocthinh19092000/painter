<template>
    <div class="header">
        <div class="logo">
            <img src="~/assets/img/logo.png" />
        </div>
        <div class="title">OTSV AI Love You</div>
    </div>
</template>
<style lang="scss" scoped>
.header {
    display: flex;
    position: relative;
    width: 1000px;
    justify-content: flex-start;
    align-items: center;
    padding: 5px 10px;
    .logo {
        img {
            width: 100px;
        }
    }
    .title {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        font-weight: 700;
        font-size: 40px;
        color: #BD0F72;
    }
}
</style>