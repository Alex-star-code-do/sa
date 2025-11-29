<template>
  <form @submit.prevent="calc" class="form">
    <UIInput
      v-model="ip"
      :error="ip !== '' && !isIpValid(ip)"
      placeholder="192.168.1.150"
    />
    <UISelect v-model="mask" :options="masks" />
    <UIButton :disabled="!isIpValid(ip)">Рассчитать</UIButton>
  </form>

  <div v-if="show" class="res">
    <div>IP: {{ ip }}</div>
    <div>Маска: {{ mask }}</div>
    <div>Адрес сети: {{ net }}</div>
    <div>Хостов: {{ cnt }}</div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import UIInput from '../components/UIInput.vue'
import UISelect from '../components/UISelect.vue'
import UIButton from '../components/UIButton.vue'

const masks = ['255.255.255.255', '255.255.255.254', '255.255.255.252', '255.255.255.248', '255.255.255.240', '255.255.255.224', '255.255.255.192', '255.255.255.128', '255.255.255.0', '255.255.254.0', '255.255.252.0', '255.255.248.0', '255.255.240.0', '255.255.224.0', '255.255.192.0', '255.255.128.0', '255.255.0.0', '255.254.0.0', '255.252.0.0', '255.248.0.0', '255.240.0.0', '255.224.0.0', '255.192.0.0', '255.128.0.0', '254.0.0.0', '252.0.0.0', '248.0.0.0', '240.0.0.0', '224.0.0.0', '192.0.0.0', '128.0.0.0', '0.0.0.0']

const ip = ref('')
const mask = ref('255.255.255.0')
const show = ref(false)

function isIpValid(ip: string): boolean {
  return /^(\d{1,3})\.(\d{1,3})\.(\d{1,3})\.(\d{1,3})$/.test(ip) &&
    ip.split('.').every(o => {
      const n = Number(o)
      return n >= 0 && n <= 255
    })
}

function getNetworkAdress(ip: string, mask: string): string {
  const i = ip.split('.').map(Number)
  const m = mask.split('.').map(Number)
  return i.map((x, j) => x & m[j]).join('.')
}

function getAddressesCount(mask: string): number {
  let b = ''
  for (const o of mask.split('.')) {
    b += Number(o).toString(2).padStart(8, '0')
  }
  const zeros = b.split('').filter(x => x === '0').length
  return zeros === 0 ? 1 : zeros === 1 ? 2 : 2 ** zeros - 2
}

const calc = () => {
  if (isIpValid(ip.value)) show.value = true
}

const net = computed(() => getNetworkAdress(ip.value, mask.value))
const cnt = computed(() => getAddressesCount(mask.value))
</script>

<style scoped>
.form {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}
.res {
  padding: 16px;
  background: var(--color-white);
  border-radius: 4px;
}
</style>
