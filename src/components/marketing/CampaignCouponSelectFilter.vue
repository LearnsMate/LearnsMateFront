<template>
  <div class="coupon-select-filter-card">
    <div class="coupon-select-section-header">
    </div>

    <div class="coupon-select-filter-container">
      <div class="coupon-select-filter-row gray">
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 이름</span>
            <input 
              v-model="filters.coupon_name"
              type="text" 
              placeholder="쿠폰 이름을 입력하세요"
              class="coupon-select-filter-input"
            />
        </div>
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 내용</span>
            <input 
              v-model="filters.coupon_contents"
              type="text" 
              placeholder="쿠폰 내용을 입력하세요"
              class="coupon-select-filter-input"
            />
        </div>
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 종류</span>
            <select
              v-model="filters.coupon_category_name"
              class="coupon-select-filter-input">
              <option value = "">전체</option>
              <option value = "일반">일반</option>
              <option value = "기념일">기념일</option>
              <option value = "신규가입">신규가입</option>
              <option value = "첫구매">첫 구매</option>
              <option value = "복귀">복귀</option>
              <option value = "완강">완강</option>
              <option value = "이벤트">이벤트</option>
            </select>
        </div>
      </div>
      <div class="coupon-select-filter-row white">
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 상태</span>
            <select
              v-model="filters.coupon_flag"
              class="coupon-select-filter-input">
              <option value = "">전체</option>
              <option value = true>활성화</option>
              <option value = false>비활성화</option>
            </select>
        </div>
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 할인율</span>
            <div class="coupon-select-discount-rate-container">
            <input 
              v-model="filters.min_discount_rate"
              type="number" 
              class="coupon-select-filter-input discount-input"
            />
            <span class="discount-rate-separator">~</span>
            <input 
              v-model="filters.max_discount_rate"
              type="number" 
              class="coupon-select-filter-input discount-input"
            />
            </div>
        </div>
        <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 시작일</span>
            <div class="coupon-select-date-range-container">
            <input 
              v-model="filters.start_coupon_start_date"
              type="date" 
              class="coupon-select-filter-input date-input"
            />
            <span class="coupon-select-date-separator">~</span>
            <input 
              v-model="filters.end_coupon_start_date"
              type="date" 
              class="coupon-select-filter-input date-input"
            />
            </div>
        </div>
      </div>
      <div class="coupon-select-filter-row gray">
      <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 만료일</span>
          <div class="coupon-select-date-range-container">
            <input 
              v-model="filters.start_expire_date"
              type="date" 
              class="coupon-select-filter-input date-input"
            />
            <span class="coupon-select-date-separator">~</span>
            <input 
              v-model="filters.end_expire_date"
              type="date"
              class="coupon-select-filter-input date-input"
            />
          </div>
      </div>
      <div class="coupon-select-filter-item">
          <span class="coupon-select-filter-label">쿠폰 생성일</span>
          <div class="coupon-select-date-range-container">
            <input 
              v-model="filters.start_created_at"
              type="date" 
              class="coupon-select-filter-input date-input"
            />
            <span class="coupon-select-date-separator">~</span>
            <input 
              v-model="filters.end_created_at"
              type="date" 
              class="coupon-select-filter-input date-input"
            />
          </div>
      </div>
      <div class="coupon-select-filter-item">
          <div class="coupon-select-button-group">
          <button @click="search" class="coupon-select-search-button">
            <i class="fas fa-search"></i>
            <img class="search-img" src="/src/assets/icons/search_white.svg" alt="">조회
          </button>
          <button @click="reset" class="coupon-select-reset-button">
            <img class="reset-img" src="/src/assets/icons/reset.svg" alt="">
          </button>
        </div>
      </div>
  </div>
  <div class="coupon-select-filter-row white">
      </div>
      </div>
  </div>
</template>


<script setup>
import { ref, defineEmits  } from 'vue'

const filters = ref({
  coupon_name: '',
  coupon_contents: '',
  coupon_category_name: '',
  coupon_flag: '',
  min_discount_rate: '',
  max_discount_rate: '',
  start_coupon_start_date: '',
  end_coupon_start_date: '',
  start_expire_date: '',
  end_expire_date: '',
  start_created_at: '',
  end_created_at: '',
  admin_code: '',
  tutor_code: '',
  registration_type: 'admin',
})

const emit = defineEmits(['search', 'reset'])

const search = () => {
  emit('search', filters.value)
}

const reset = () => {
  Object.keys(filters.value).forEach(key => {
    filters.value[key] = ''
  })
  emit('reset')
}
</script>

<style scoped>
.coupon-select-filter-card {
  margin-bottom: 16px;
  background-color: white;
  padding: 0;
}

.coupon-select-section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0px 10px;
  border-bottom: 1px solid #e9ecef;
}

.coupon-select-section-title {
  font-size: 17px;
  font-weight: bold;
}

.coupon-select-filter-container {
  display: flex;
  flex-direction: column;
}

.coupon-select-filter-row {
  display: flex;
  padding: 3px 10px;
}

.coupon-select-filter-row.gray {
  background-color: #EFEFEF;
  border-top: #D9D9D9;
  border-bottom: #D9D9D9;
}

.coupon-select-filter-row.white {
  background-color: white;
}

.coupon-select-filter-item {
  width: 35%;
  padding-left: 8px;
  display: flex;
  align-items: center;
}

.coupon-select-partial-width {
  width: 33.33%;
  flex: 0 0 33.33%;
}
 
.coupon-select-filter-label {
  width: 5rem;
  min-width: 5rem;
  font-size: 11px;
  font-weight: 500;
  text-align: end;
  padding-right: 10px;
}

.coupon-select-filter-input {
  flex: 1;
  padding: 5px 5px;
  font-size: 11px;
  border: 1px solid #e2e8f0;
  min-width: 0;
  width: 100%;
  outline: none;
}

.coupon-select-date-range-container,
.coupon-select-discount-rate-container {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.coupon-select-date-input,
.coupon-select-discount-input {
  flex: 1;
}

.coupon-select-date-separator,
.coupon-select-discount-rate-separator {
   color: #64748b;
    padding: 0 0.25rem;
}

.coupon-select-button-group {
  display: flex;
  gap: 0.5rem;
  margin-left: 310px;
}

.coupon-select-search-button {
  padding: 2px 6px 3px 3px;        
  background-color: #005950;
  border: 1px solid #005950;
  border-radius: 4px;
  font-size: 11px;
  color: white;
  display: flex;
  align-items: center;
  margin-bottom: 4px;
  margin-top: 4px;
}

.coupon-select-search-button:hover {
  background-color: #004c42;  
}

.coupon-select-reset-button {
  padding: 4px 5px 3px;   
  border: 1px solid #A29D9D;
  border-radius: 4px;
  font-size: 11px;
  background-color: white;
  margin-bottom: 4px;
  margin-top: 4px;
}

.coupon-select-reset-button:hover {
  background-color: #f8fafc;
}

.coupon-select-search-button:focus,
.coupon-select-reset-button:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(13, 148, 136, 0.2);
}

input:focus {
  outline: none; 
}
</style>
