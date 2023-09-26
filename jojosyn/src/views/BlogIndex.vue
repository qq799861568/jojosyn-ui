<template>
    <!-- <div class="common-layout">
        <el-container class="debug-outline">
            <el-header>Header</el-header>
            <el-container>
                <el-container>
                    <el-main>Main</el-main>
                    <el-footer>Footer</el-footer>
                </el-container>
                <el-aside width="200px">Aside</el-aside>
            </el-container>
        </el-container>
    </div> -->

    <div class="debug-outline">
        <el-row class="header">
            <el-col :span="14" :offset="4">
                <Header/>
            </el-col>
        </el-row>
        <el-divider />

        <el-row >

            <el-col class="main" :span="9" :offset="5">
                <RouterView />

                <!-- <BlogPreview />
                <BlogPreview/>
                <BlogPreview/> -->
            </el-col>
            <el-col class="aside" :span="5" :offset="1">
                <Aside/>
            </el-col>
        </el-row>
        <el-divider />

        <el-row class="footer">
            <el-col :span="14" :offset="4">
                <Footer/>

            </el-col>
        </el-row>

    </div>
</template>
  
<style>

/* .debug-outline,
.debug-outline * {
    outline: 2px solid blue;
} */
</style>

<script setup>
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'
import Aside from '../components/Aside.vue'
import { RouterLink, RouterView } from 'vue-router'

</script>