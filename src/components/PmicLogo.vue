<template>
    <div class="logo" id="logo">
        <svg width="70" height="70" viewBox="0 0 70 70" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g id="Group 3677">
            <g id="Group 3652">
            <rect id="Rectangle 48" width="70" height="70" fill="#EB6000"/>
            </g>
            <g id="Group 3653">
            <path id="Vector" d="M13.75 56.25H35V35H13.75L13.75 56.25Z" fill="#FFF0E6"/>
            <path id="Vector_2" d="M35 56.25H56.25V35H35V56.25Z" fill="white"/>
            <path id="Vector_3" d="M13.75 35H35L24.3758 13.75L13.75 35Z" fill="#FFF0E6"/>
            <path id="Vector_4" d="M35.0155 35H56.25L45.6095 13.75H24.375L35.0155 35Z" fill="#5DA1FF"/>
            </g>
            </g>
        </svg>
        <h1>PMIC AI</h1>
    </div>
</template>

<script setup lang="ts">
</script>

<style scoped lang="scss">
.logo{
    display: flex;
    align-items: center;
    color: $colorOrange;
}
h1{
    font-size: 24px;
    margin-left: 16px;
    @media (min-width: 1921px) {
        font-size: 1.2vw;
        margin-left: .8vw;
    }
}
</style>