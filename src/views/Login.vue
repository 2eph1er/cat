<template>
    <div id="login" class="container mt-3 py-5">
        <div class="row">
            <div class="col-12 col-md-8 col-lg-6 mx-auto animate__animated animate__fadeIn">
                <div class="card h-100 p-5 rounded-5 card-bg">
                    <h1 class="text-center mt-auto fw-bold">猫咪身份识别</h1>
                    <p class="text-center text-muted">欢迎回来，请登录您的账号</p>

                    <div class="d-flex flex-column my-4 align-items-center justify-content-center">
                        <img src="@/assets/logo.png" class="img-fluid rounded-circle border border-2 p-1 object-fit-cover" style="height: 120px; width: 120px;" />
                        
                        <form class="w-100 mt-4" @submit.prevent="handleLogin">
                            <div class="mb-3">
                                <label for="username" class="form-label">用户名</label>
                                <input 
                                    type="text" 
                                    class="form-control rounded-3" 
                                    id="username" 
                                    v-model="username"
                                    placeholder="请输入用户名"
                                    required
                                />
                            </div>
                            <div class="mb-4">
                                <label for="password" class="form-label">密码</label>
                                <input 
                                    type="password" 
                                    class="form-control rounded-3" 
                                    id="password" 
                                    v-model="password"
                                    placeholder="请输入密码"
                                    required
                                />
                            </div>
                            <div class="d-flex justify-content-between align-items-center mb-3">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" v-model="rememberMe" id="rememberMe">
                                    <label class="form-check-label" for="rememberMe">记住我</label>
                                </div>
                                <a href="#" class="text-decoration-none">忘记密码?</a>
                            </div>
                            <button type="submit" class="btn btn-primary w-100 py-2 rounded-3 mt-2" :disabled="isLoading">
                                <span v-if="isLoading">登录中...</span>
                                <span v-else>登录</span>
                            </button>
                        </form>
                    </div>

                    <p class="text-center text-muted mt-3">
                        还没有账号? <a href="#" class="text-decoration-none" @click.prevent="goToRegister">立即注册</a>
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const username = ref('');
const password = ref('');
const rememberMe = ref(false);
const isLoading = ref(false);

const handleLogin = async () => {
    try {
        isLoading.value = true;
        // 这里实现登录逻辑
        console.log('登录信息:', {
            username: username.value,
            password: password.value,
            rememberMe: rememberMe.value
        });
        
        // 模拟登录延迟
        await new Promise(resolve => setTimeout(resolve, 1000));
        
        // 登录成功后跳转到仪表盘
        router.push('/dashboard');
    } catch (error) {
        console.error('登录失败:', error);
    } finally {
        isLoading.value = false;
    }
};

const goToRegister = () => {
    router.push('/register');
};
</script>

<style scoped lang="css">
.card-bg {
    background-color: #fef4ea;
}

.btn-primary {
    background-color: #f8954f;
    border-color: #f8954f;
}

.btn-primary:hover, .btn-primary:focus {
    background-color: #e68340;
    border-color: #e68340;
}

a {
    color: #f8954f;
}

a:hover {
    color: #e68340;
}
</style>