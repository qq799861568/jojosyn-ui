<template>
    <div class="blog">
        
        <el-row class="blog-title">
            <el-col>
                异步场景上下文传递方案
            </el-col>
        </el-row>
        <el-row class="blog-content">
            <el-col>
                在 Spring 项目中，要在异步场景下获取业务的上下文，可以考虑使用以下几种方案：

ThreadLocal： Spring 提供了一个 ThreadLocal 类型的 RequestContextHolder，可以将当前线程的请求上下文信息存储在 ThreadLocal 中，然后在异步任务中获取。这适用于在同一线程中传递上下文信息。

java
Copy code
// 在业务代码中设置上下文
RequestContextHolder.setRequestAttributes(RequestContextHolder.currentRequestAttributes());

// 在异步任务中获取上下文
RequestAttributes requestAttributes = RequestContextHolder.getRequestAttributes();
使用 InheritableThreadLocal： 如果你的异步任务创建了新的线程，而你希望在子线程中也能获取到父线程的上下文信息，可以考虑使用 InheritableThreadLocal 而不是普通的 ThreadLocal。

java
Copy code
// 在业务代码中设置上下文
InheritableRequestContextHolder.setRequestAttributes(RequestContextHolder.currentRequestAttributes());

// 在异步任务中获取上下文
RequestAttributes requestAttributes = InheritableRequestContextHolder.getRequestAttributes();
使用 @Async 和自定义 AsyncConfigurer： Spring 提供了 @Async 注解来标记异步方法，但是默认情况下不会继承父线程的上下文信息。你可以通过实现 AsyncConfigurer 接口来自定义异步执行的方式，以便将上下文信息传递给异步任务。

java
Copy code
@Configuration
@EnableAsync
public class AsyncConfig implements AsyncConfigurer {

    @Override
    public Executor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setTaskDecorator(new ContextCopyingDecorator());
        executor.initialize();
        return executor;
    }
}

public class ContextCopyingDecorator implements TaskDecorator {

    @Override
    public Runnable decorate(Runnable runnable) {
        RequestAttributes context = RequestContextHolder.getRequestAttributes();
        return () -> {
            try {
                RequestContextHolder.setRequestAttributes(context);
                runnable.run();
            } finally {
                RequestContextHolder.resetRequestAttributes();
            }
        };
    }
}
无论哪种方案，都需要小心处理上下文信息的管理，避免资源泄漏或者错误的上下文传递。选择合适的方案取决于你的具体需求和项目架构。
            </el-col>
        </el-row>
    </div>
</template>

<style scoped>
.blog {
    margin-bottom: 20px;
}

</style>

<script setup>
import { onMounted } from 'vue';


onMounted(()=> {
    console.log("进入博客主页，要执行查询");

})

</script>