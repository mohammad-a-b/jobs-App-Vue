<template>
  <div class="job-list">
    <h2>شغل‌ها</h2>
    <div v-if="loading">در حال بارگذاری...</div>
    <div v-for="job in jobs" :key="job.id" class="job-item">
      <div class="name-and-logo">
        <img :src="job.companyId.logo" alt="لوگوی شرکت" class="company-logo" />
        <p class="company-title">{{ job.companyId.title }}</p>
      </div>
      <h3 :class="{ urgent: job.immediateRequirement }">
        {{ job.skills.join(", ") }}
      </h3>
      <div class="description">
        <p>{{ job.remotePossibility ? "دورکاری" : "حضوری" }}</p>
        <p>
          . | {{ job.salary === 0 ? "توافقی" : job.salary + " میلیون تومان" }}
        </p>
      </div>
    </div>
    <router-link to="/jobs/create">برو به صفحه ایجاد</router-link>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const jobs = ref([]);
const loading = ref(true);

const fetchJobs = async () => {
  try {
    const response = await fetch("http://185.45.194.24:3000/api/jobs");
    if (!response.ok) throw new Error("خطا در بارگذاری شغل‌ها");
    jobs.value = await response.json();
  } catch (err) {
    console.error(err);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchJobs);
</script>

<style scoped>
.job-list {
  margin: 0 auto;
  max-width: 400px;
  padding: 20px 16px;
  margin-top: 30px;
  border: 1px solid #000000;
  background-color: #f2f2f7;
  border-radius: 24px;
  box-shadow: 0px 9px 50px rgba(0, 0, 0, 0.43);
}
.job-item {
  margin-bottom: 15px;
  padding: 12px;
  background-color: #fff;
  border: 1px solid #000000;
  border-radius: 12px;
}
.company-title {
  font-size: 12px;
  font-weight: 400;
}
.company-logo {
  width: 32px; 
  aspect-ratio: 1/1;
  border-radius: 50%;
}
.description p {
  font-size: 14px;
  font-weight: 300;
  color: #8e8e93;
}
.description {
  display: flex;
  justify-content: end;
  align-items: end;
}
h3 {
  margin-top: 7px;
}
.urgent {
  color: #ff3b30;
}
.name-and-logo{
  display: flex;
  align-items: center;
  gap: 6px;
}
</style>
