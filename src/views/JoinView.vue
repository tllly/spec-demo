<script setup>
import { reactive, ref } from 'vue';

const jobs = [
  {
    title: '前端开发工程师',
    description: '使用 Vue 3 和 现代 CSS 构建美观且高性能的用户界面。',
  },
  {
    title: '后端开发工程师',
    description: '使用 Node.js 或 Python 设计并实现可扩展的 API 和微服务。',
  },
  {
    title: 'UI/UX 设计师',
    description: '为我们的产品创建直观的用户体验和视觉效果出众的设计。',
  },
];

const form = reactive({
  name: '',
  email: '',
  position: '',
});

const errors = reactive({
  name: '',
  email: '',
  position: '',
});

const isSubmitting = ref(false);

const validateEmail = (email) => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return re.test(email);
};

const handleSubmit = () => {
  // 重置错误信息
  errors.name = '';
  errors.email = '';
  errors.position = '';

  let isValid = true;

  if (!form.name.trim()) {
    errors.name = '请填写姓名';
    isValid = false;
  }

  if (!form.email.trim()) {
    errors.email = '请填写电子邮箱';
    isValid = false;
  } else if (!validateEmail(form.email)) {
    errors.email = '电子邮箱格式不正确';
    isValid = false;
  }

  if (!form.position) {
    errors.position = '请选择一个职位';
    isValid = false;
  }

  if (isValid) {
    isSubmitting.value = true;
    // 模拟 API 调用
    setTimeout(() => {
      alert(`提交成功！感谢您的申请，${form.name}。我们会尽快联系您。`);
      form.name = '';
      form.email = '';
      form.position = '';
      isSubmitting.value = false;
    }, 1000);
  }
};
</script>

<template>
  <div class="join-page">
    <!-- 介绍部分 -->
    <section class="intro container">
      <h1 class="section-title">加入我们的团队</h1>
      <p class="intro-text">
        在 Tang，我们正在构建技术的未来。我们正在寻找有激情、想要有所作为并与我们共同成长的伙伴。
        加入一个充满创新、协作和持续学习氛围的文化。
      </p>
    </section>

    <!-- 职位列表部分 -->
    <section class="jobs container">
      <h2 class="section-title">开放职位</h2>
      <div class="job-grid">
        <div v-for="job in jobs" :key="job.title" class="job-card">
          <h3>{{ job.title }}</h3>
          <p>{{ job.description }}</p>
        </div>
      </div>
    </section>

    <!-- 申请表单部分 -->
    <section class="application container">
      <h2 class="section-title">立即申请</h2>
      <form @submit.prevent="handleSubmit" class="apply-form">
        <div class="form-group">
          <label for="name">姓名</label>
          <input 
            type="text" 
            id="name" 
            v-model="form.name" 
            :class="{ 'error-input': errors.name }"
            placeholder="您的全名"
          >
          <span v-if="errors.name" class="error-text">{{ errors.name }}</span>
        </div>

        <div class="form-group">
          <label for="email">电子邮箱</label>
          <input 
            type="email" 
            id="email" 
            v-model="form.email" 
            :class="{ 'error-input': errors.email }"
            placeholder="your.email@example.com"
          >
          <span v-if="errors.email" class="error-text">{{ errors.email }}</span>
        </div>

        <div class="form-group">
          <label for="position">申请职位</label>
          <select 
            id="position" 
            v-model="form.position" 
            :class="{ 'error-input': errors.position }"
          >
            <option value="" disabled>选择一个职位</option>
            <option v-for="job in jobs" :key="job.title" :value="job.title">
              {{ job.title }}
            </option>
          </select>
          <span v-if="errors.position" class="error-text">{{ errors.position }}</span>
        </div>

        <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
          {{ isSubmitting ? '提交中...' : '提交申请' }}
        </button>
      </form>
    </section>
  </div>
</template>

<style scoped>
.join-page {
  padding: 4rem 0;
}

.intro {
  text-align: center;
  margin-bottom: 5rem;
}

.intro-text {
  max-width: 800px;
  margin: 0 auto;
  font-size: 1.2rem;
  color: var(--gray-dark);
}

.job-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 5rem;
}

.job-card {
  padding: 2rem;
  background: var(--bg-color);
  border-radius: 12px;
  box-shadow: var(--shadow);
  transition: var(--transition);
}

.job-card:hover {
  transform: translateY(-5px);
}

.job-card h3 {
  color: var(--primary-color);
  margin-bottom: 1rem;
}

.apply-form {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  background: var(--gray-light);
  border-radius: 12px;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.form-group input,
.form-group select {
  width: 100%;
  padding: 0.8rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
}

.error-input {
  border-color: #ff4d4f !important;
}

.error-text {
  color: #ff4d4f;
  font-size: 0.85rem;
  margin-top: 0.25rem;
  display: block;
}

.btn-primary {
  width: 100%;
  margin-top: 1rem;
}

.btn-primary:disabled {
  background-color: var(--gray-dark);
  border-color: var(--gray-dark);
  cursor: not-allowed;
  transform: none;
}
</style>
