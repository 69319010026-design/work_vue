<template>
    <div class="main-wrapper">
        <h1>สมัครสมาชิก</h1>
        <form @submit="alert_data">
            <div class="form-group">
                <label>ชื่อ:</label>
                <input type="text" v-model="name_box" placeholder="กรอกชื่อ" />
            </div>
            <div class="form-group">
                <label>นามสกุล:</label>
                <input type="text" v-model="surname_box" placeholder="กรอกนามสกุล" />
            </div>
            <div class="form-group">
                <label>เพศ:</label>
                <label>
                    <input type="radio" name="sex" v-model="sex" value="male"> ชาย
                </label>

                <label>
                    <input type="radio" name="sex" v-model="sex" value="female"> หญิง
                </label>
            </div>
            <div class="form-group">
                <label>งานอดิเรก</label>
                <label>
                    <input type="checkbox" name="favorite" v-model="favorite" value="เลี้ยงสัตว์"> เลี้ยงสัตว์
                </label>

                <label>
                    <input type="checkbox" name="favorite" v-model="favorite" value="วาดรูป"> วาดรูป
                </label>

                <label>
                    <input type="checkbox" name="favorite" v-model="favorite" value="เล่นดนตรี"> เล่นดนตรี
                </label>

                <label>
                    <input type="checkbox" name="favorite" v-model="favorite" value="ต่อยมวย"> ต่อยมวย
                </label>
            </div>
            <div class="form-group">
                <button type="submit">Click</button>

            </div>

        </form>




    </div>
</template>
<script setup>
//เขียนโปรแกรม แบบ javascript
import { ref } from 'vue';
const name_box = ref('');
const surname_box = ref('');
const sex = ref('');
const favorite = ref([])
const alert_data = () => {
    alert('ยินดีต้อนรับ คุณ' + name_box.value + ' ' + surname_box.value + ' ' + 'เพศ' + sex.value + ' ' + 'งานอดิเรก' + favorite.value);

}
</script>
<style scoped>
/*ตกแต่ง frontend ใช้ css */
.main-wrapper {
    width: 1200px;
    margin: 40px auto;
    padding: 30px;
    background-color: #f4f7f6;
    /* สีเทาอ่อนอมฟ้า สบายตา */
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
    font-family: sans-serif;
}

้้h1 {
    font-size: larger;
    color: brown;
}

.form-group {
    margin-bottom: 15px;
}
</style>