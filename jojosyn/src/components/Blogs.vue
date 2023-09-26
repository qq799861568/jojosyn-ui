<template>
    <div class="blog" v-for="o in 3" :key="o">
        <el-card class="box-card">
            <template #header>
                <div class="card-header">
                    <el-link :underline="false">

                        <span class="blog-title">{{ blog.title + o }}</span>
                    </el-link>
                </div>
            </template>
            <div class="text item">{{ blog.content + o }}</div>
        </el-card>
    </div>
</template>

<style scoped>
.blog {
    margin-bottom: 20px;
}
.blog-title {
    font-size: 150%;
}
</style>
<script setup>
import { RouterLink, RouterView } from 'vue-router'
// 响应式状态
const blog = {
    title: "异步场景上下文传递方案",
    content: "在 Spring 项目中，要在异步场景下获取业务的上下文，可以考虑使用以下几种方案：ThreadLocal： Spring 提供了一个 ThreadLocal 类型的 RequestContextHolder，可以将当前线程的请求上下文信息存储在 ThreadLocal中，然后在异步任务中获取。这适用于在同一线程中传递上下文信息。javaCopy code// 在业务代码中设置上下文RequestContextHolder.setRequestAttributes(RequestContextHolder.currentRequestAttributes());// 在异步任务中获取上下文RequestAttributes requestAttributes = RequestContextHolder.getRequestAttributes();使用 InheritableThreadLocal： 如果你的异步任务创建了新的线程，而你希望在子线程中也能获取到父线程的上下文信息，可以考虑使用 Inherit 。。。。"
}

</script>