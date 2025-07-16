<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="name"
        label="ชื่อ-สกุล / Your name *"
        hint="ชื่อและนามสกุล / Name and surname"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาพิมพ์ชื่อ / Please type something']"
      />

      <q-input
        filled
        type="number"
        v-model="age"
        label="อายุ:"
        lazy-rules
        :rules="[ 
          val => val !== null && val !== '' || 'กรุณาใส่อายุของคุณ / Please type your age นะครับ',
          val => val > 0 && val < 100 || 'กรุณาใส่อายุจที่ถูกต้อง / Please type a valid age (0-100) นะจ๊ะ'
        ]"
      />

      <q-toggle v-model="accept" label="ยอมรับ / I accept the license and terms" />

      <div>
        <q-btn label="ยอมรับ / Submit" type="submit" color="primary" />
        <q-btn label="ยกเลิก / Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>
  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()
    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)

    return {
      name,
      age,
      accept,
      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'คุณจำเป็นต้องยอมรับ'
          })
        } else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'ข้อมูลได้รับการยืนยัน'
          })
        }
      },
      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>
