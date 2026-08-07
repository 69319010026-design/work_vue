<template>
  <div class="main-wrapper">
    <h2>📋 ระบบเช็คชื่อเข้าชั้นเรียน</h2>

    <!-- 1. ฟอร์มกรอกข้อมูล -->
    <form @submit.prevent="addAttendance" class="form-card">
      <div class="form-group">
        <label for="fullName">ชื่อ - นามสกุล:</label>
        <input 
          id="fullName"
          v-model.trim="form.fullName" 
          type="text" 
          placeholder="กรอกชื่อ-นามสกุล" 
          required 
        />
      </div>

      <div class="form-group">
        <label for="status">สถานะ:</label>
        <select id="status" v-model="form.status">
          <option value="มาเรียน">มาเรียน</option>
          <option value="สาย">สาย</option>
          <option value="ขาดเรียน">ขาดเรียน</option>
        </select>
      </div>

      <div class="form-group">
        <label for="note">หมายเหตุ:</label>
        <input 
          id="note"
          v-model.trim="form.note" 
          type="text" 
          placeholder="ระบุเหตุผล (ถ้ามี)" 
        />
      </div>

      <button type="submit" class="btn-submit">บันทึกข้อมูล 💾</button>
    </form>

    <!-- 2. ตารางแสดงผล -->
    <div class="list-container">
      <h3>รายการผู้เข้าร่วมชั้นเรียน ({{ attendanceList.length }} คน)</h3>
      
      <table v-if="attendanceList.length > 0">
        <thead>
          <tr>
            <th>#</th>
            <th>ชื่อ-นามสกุล</th>
            <th>สถานะ</th>
            <th>หมายเหตุ</th>
            <th>จัดการ</th>
          </tr>
        </thead>
        <tbody>
          <!-- ใช้ item.id เป็น :key แทน index -->
          <tr v-for="(item, index) in attendanceList" :key="item.id">
            <td>{{ index + 1 }}</td>
            <td>{{ item.fullName }}</td>
            <td>
              <span :class="['badge', getBadgeClass(item.status)]">
                {{ item.status }}
              </span>
            </td>
            <td>{{ item.note || '-' }}</td>
            <td>
              <button @click="deleteItem(item.id)" class="btn-delete">ลบ</button>
            </td>
          </tr>
        </tbody>
      </table>

      <p v-else class="empty-text">ยังไม่มีข้อมูลการเช็คชื่อในขณะนี้</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  fullName: '',
  status: 'มาเรียน',
  note: ''
})

const attendanceList = ref([])

const addAttendance = () => {
  // เพิ่ม id แบบไม่ซ้ำเพื่อนำไปใช้เป็น :key
  attendanceList.value.push({
    id: Date.now(),
    ...form.value
  })

  // รีเซ็ตฟอร์ม
  form.value = {
    fullName: '',
    status: 'มาเรียน',
    note: ''
  }
}

// ลบข้อมูลโดยใช้ ID อ้างอิง
const deleteItem = (id) => {
  attendanceList.value = attendanceList.value.filter(item => item.id !== id)
}

const getBadgeClass = (status) => {
  switch (status) {
    case 'มาเรียน': return 'status-green'
    case 'สาย': return 'status-orange'
    case 'ขาดเรียน': return 'status-red'
    default: return ''
  }
}
</script>

<style scoped>
.main-wrapper {
  max-width: 700px;
  margin: 30px auto;
  padding: 20px;
  background-color: #f8fafc;
  border-radius: 12px;
  font-family: sans-serif;
}

.form-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.form-group {
  margin-bottom: 12px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 4px;
}

input, select {
  width: 100%;
  padding: 8px;
  border: 1px solid #cbd5e1;
  border-radius: 4px;
  box-sizing: border-box;
}

.btn-submit {
  width: 100%;
  padding: 10px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s;
}

.btn-submit:hover {
  background-color: #33a06f;
}

table {
  width: 100%;
  border-collapse: collapse;
  background: white;
}

th, td {
  padding: 10px;
  border: 1px solid #e2e8f0;
  text-align: left;
}

.badge {
  padding: 4px 8px;
  border-radius: 4px;
  color: white;
  font-size: 12px;
}
.status-green { background-color: #22c55e; }
.status-orange { background-color: #f97316; }
.status-red { background-color: #ef4444; }

.btn-delete {
  background-color: #ef4444;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 4px 8px;
  font-size: 12px;
  cursor: pointer;
}

.btn-delete:hover {
  background-color: #dc2626;
}

.empty-text {
  text-align: center;
  color: #64748b;
}
</style>