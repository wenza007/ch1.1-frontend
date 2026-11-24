<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">
      Version Control + Docker Demo (Quasar)
    </div>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow (ตัวอย่างขั้นตอนทำงาน)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts (สรุปสั้น ๆ)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card>
      <q-card-section>
        <div class="text-h6">Docker Quick Reference (คำสั่งที่ใช้บ่อย)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(cmd, index) in dockerCommands" :key="index">
            <q-item-section>
              <q-item-label class="text-weight-medium">{{ cmd.command }}</q-item-label>
              <q-item-label caption>{{ cmd.whenToUse }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
const gitSteps = [
  {
    title: 'แก้โค้ด Quasar ใน src/',
    detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ',
  },
  {
    title: 'ตรวจสอบสถานะไฟล์',
    detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง',
  },
  {
    title: 'เพิ่มไฟล์เข้า staging',
    detail: 'จากรากโปรเจกต์ ใช้ git add frontend/src/pages/IndexPage.vue',
  },
  {
    title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits',
    detail: 'เช่น `feat: add Git workflow demo page`',
  },
  {
    title: 'push ขึ้น GitHub',
    detail: 'ใช้ git push -u origin feature/quasar-demo แล้วเปิด Pull Request',
  },
]

const dockerItems = [
  {
    title: 'Image',
    detail: 'แพ็กเกจที่มีไฟล์และการตั้งค่าที่ใช้สร้าง container เช่น image ที่รวม Quasar SPA กับ Nginx',
  },
  {
    title: 'Container',
    detail: 'อินสแตนซ์ที่สร้างจาก image เช่น container ที่รัน Nginx เพื่อเสิร์ฟไฟล์ Quasar',
  },
  {
    title: 'Volume',
    detail: 'เก็บข้อมูลให้คงอยู่แยกจากวงจรชีวิตของ container เช่น ไฟล์อัปโหลดของ backend',
  },
  {
    title: 'Network',
    detail: 'ให้บริการใน Docker ติดต่อกันได้ เช่น Nginx ส่งต่อคำขอไปยัง Express',
  },
]

const dockerCommands = [
  {
    command: 'docker compose up -d --build',
    whenToUse: 'ใช้เมื่อต้องการสร้าง image ใหม่ตาม Dockerfile แล้วเปิดรันทุก service แบบเบื้องหลัง (-d)',
  },
  {
    command: 'docker compose ps',
    whenToUse: 'ใช้เมื่อต้องการตรวจสอบสถานะและพอร์ตของ container ทั้งหมดในโปรเจกต์ว่าทำงานอยู่หรือไม่',
  },
  {
    command: 'docker compose logs -f',
    whenToUse: 'ใช้เมื่อต้องการดู log แบบเรียลไทม์เพื่อดีบักตอนแอปหรือ Nginx/Express มีปัญหา',
  },
  {
    command: 'docker compose down',
    whenToUse: 'ใช้เมื่อต้องการหยุดและลบ container รวมถึง network ที่ compose สร้างไว้เมื่อเลิกใช้งานชั่วคราว',
  },
  {
    command: 'docker ps -a',
    whenToUse: 'ใช้เมื่อต้องการดูรายการ container ทั้งหมดในเครื่อง (รวมตัวที่หยุดทำงานหรือ exit ไปแล้ว)',
  },
]
</script>