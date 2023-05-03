<template>
  <header class="titleDiv d-flex justify-content-center pt-2">
    <h3 class="titl text-white fs-1">Build Your Own PC</h3>
  </header>
  <div class="d-flex flex-column mainBody">
    <div class="d-flex flex-column p-2">
      <p class="fs-3">step1: Select your CPU</p>
      <div class="d-flex">
        <div class="d-flex align-items-center">
          <p class="fs-4 me-2">Brand</p>
          <select name="cpuBrands" class="select" v-model="cpuSelBrand">
            <option v-for="cpuBrand in cpuBrands" :value="cpuBrand">
              {{ cpuBrand }}
            </option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4 me-2">Model</p>
          <select name="cpuModels" class="select" v-model="cpuResModel">
            <option v-for="model in cpuModels">{{ model }}</option>
          </select>
        </div>
      </div>
    </div>
    <div class="d-flex flex-column p-2">
      <p class="fs-3">step2: Select your GPU</p>
      <div class="d-flex">
        <div class="d-flex align-items-center">
          <p class="fs-4">Brand</p>
          <select name="gpuBrands" class="select innerSpace" v-model="gpuSelBrand">
            <option v-for="brand in gpuSelBrands">{{ brand }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Model</p>
          <select name="gpuModels" class="select innerSpace" v-model="gpuResModel">
            <option v-for="model in gpuModels">{{ model }}</option>
          </select>
        </div>
      </div>
    </div>
    <div class="d-flex flex-column p-2">
      <p class="fs-3">step3: Select your memory card</p>
      <div class="d-flex">
        <div class="d-flex align-items-center">
          <p class="fs-4">How Many?</p>
          <select name="manyRams" class="mb-3 innerSpace" v-model="manyRam">
            <option v-for="nums in manyRams" :key="nums">{{ nums }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Brand</p>
          <select name="ramBrands" class="select innerSpace" v-model="ramBrand">
            <option v-for="brand in ramBrands" :value="brand">{{ brand }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Model</p>
          <select name="ramModels" class="select innerSpace" v-model="ramResModel">
            <option v-for="model in ramModels">{{ model }}</option>
          </select>
        </div>
      </div>
    </div>
    <div class="d-flex flex-column p-2">
      <p class="fs-3">step4: Select your storage</p>
      <div class="d-flex">
        <div class="d-flex align-items-center">
          <p class="fs-4">HDD or SSD</p>
          <select name="hddOrsdd" class="select innerSpace" v-model="selhddOrssdes">
            <option v-for="ssdOrhdd in selhddOrssd" :key="ssdOrhdd">{{ ssdOrhdd }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Storage</p>
          <select name="manyStorage" class="select innerSpace" v-model="storageCapes">
            <option v-for="cap in storageCap">{{ cap }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Brand</p>
          <select name="ssdBrands" class="select innerSpace" v-model="storageSelBrandes">
            <option v-for="brands in storageSelBrand">{{ brands }}</option>
          </select>
        </div>
        <div class="d-flex align-items-center outerSpace">
          <p class="fs-4">Model</p>
          <select name="ssdModels" class="select innerSpace" v-model="storageSelModeles">
            <option v-for="models in storageSelModel">{{ models }}</option>
          </select>
        </div>
      </div>
    </div>
    <div class="p-4 d-flex">
      <button class="btn btn-primary fs-4 col-3" @click="addBtn">Add PC</button>
    </div>
  </div>
  <div v-if="isAdded" class="d-flex mt-5 justify-content-center">
    <div class="d-flex flex-column bg-info text-white col-sm-6 rounded-4 resSpace">
      <div class="d-flex flex-column pt-3">
        <p class="fs-2">CPU</p>
        <p class="fs-5">Brnad: {{ cpuBrand }}</p>
        <p class="fs-5">Model: {{ cpuModel }}</p>
      </div>
      <div class="d-flex flex-column">
        <p class="fs-2">GPU</p>
        <p class="fs-5">Brnad:{{ gpuBrand }}</p>
        <p class="fs-5">Model:{{ gpuModel }}</p>
      </div>
      <div>
        <p class="fs-1">RAM</p>
        <p class="fs-5">Brnad:{{ ramBrandes }}</p>
        <p class="fs-5">Model:{{ ramModel }}</p>
      </div>
      <div>
        <p class="fs-2">Storage</p>
        <p class="fs-5">Disk:{{ reshddOrssd }}</p>
        <p class="fs-5">Storage:{{ resStorage }}</p>
        <p class="fs-5">Brand:{{ resStoBrand }}</p>
        <p class="fs-5">Model: {{ resStoModel }}</p>
      </div>
      <div>
        <p class="fs-2">Game: {{ resGaming }}%</p>
      </div>
      <div>
        <p class="fs-2">Work: {{ resWorking }}%</p>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import axios, { type AxiosResponse } from 'axios'
import { defineComponent, onMounted, ref, watch, type Ref } from 'vue'
export default defineComponent({
  name: 'MainView',
  setup() {
    const isAdded: Ref<boolean> = ref(false)
    const cpuBrand: Ref<string> = ref('')
    const cpuModel: Ref<string> = ref('')
    const gpuBrand: Ref<string> = ref('')
    const gpuModel: Ref<string> = ref('')
    const ramBrandes: Ref<string> = ref('')
    const ramModel: Ref<string> = ref('')
    const reshddOrssd: Ref<string> = ref('')
    const resStorage: Ref<string> = ref('')
    const resStoBrand: Ref<string> = ref('')
    const resStoModel = ref('')
    const resGaming: Ref<string[] | any> = ref('')
    const resWorking: Ref<string[] | any> = ref('')
    const resultData: Ref<string[] | any> = ref('')
    // CPU
    const cpuBrands: Ref<string[] | any> = ref([])
    const cpuSelBrand: Ref<string[] | any> = ref([])
    const cpuModels: Ref<string[] | any> = ref([])
    const cpuResModel: Ref<string[] | any> = ref([])
    // GPU
    const gpuSelBrands: Ref<string[] | any> = ref([])
    const gpuSelBrand: Ref<string[] | any> = ref([])
    const gpuModels: Ref<string[] | any> = ref([])
    const gpuResModel: Ref<string[] | any> = ref([])
    // Mmeory Card
    const manyRam: Ref<string[] | any> = ref([])
    const manyRams: Ref<string[] | any> = ref([])
    const ramBrand: Ref<string[] | any> = ref([])
    const ramBrands: Ref<string[] | any> = ref([])
    const ramModels: Ref<string[] | any> = ref([])
    const ramResModel: Ref<string[] | any> = ref([])
    // storage
    const selhddOrssd: Ref<string[] | any> = ref([])
    const selhddOrssdes: Ref<string[] | any> = ref([])
    const storageCap: Ref<string[] | any> = ref([])
    const storageCapes: Ref<string[] | any> = ref([])
    const storageSelBrand: Ref<string[] | any> = ref([])
    const storageSelBrandes: Ref<string[] | any> = ref([])
    const storageSelModel: Ref<string[] | any> = ref([])
    const storageSelModeles: Ref<string[] | any> = ref([])
    onMounted(async () => {
      // CPU
      const cpu: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=cpu`
      )
      const cpuSelBrands: Set<number> = new Set(cpu.data.map((computer: any) => computer.Brand))
      cpuBrands.value = Array.from(cpuSelBrands)
      // GPU
      const gpu: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=gpu`
      )
      const gpuSelBrand: Set<number> = new Set(
        gpu.data.map((computer: any) => computer.Brand).sort()
      )
      gpuSelBrands.value = Array.from(gpuSelBrand)
      // Memory Card
      const ram: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=ram`
      )
      // storage
      const ssd: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=ssd`
      )
      const hdd: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=hdd`
      )
      // ram(How many)
      const nums: Set<number> = new Set(
        ram.data
          .map((computer: string | any) => {
            const com: string = computer.Model
            const manyRams: number = parseInt(
              com.slice(-6, com.length).replace(' ', '').slice(0, 1),
              10
            )
            return manyRams
          })
          .sort()
      )
      manyRams.value = Array.from(nums)
      // ram(Brand)
      const ramSelBrand: Set<number> = new Set(
        ram.data.map((computer: any) => computer.Brand).sort()
      )
      ramBrands.value = Array.from(ramSelBrand)
      // storage(HDD or SDD)
      const selSsd: string = ssd.data[0].Type
      const selHdd: string = hdd.data[0].Type
      selhddOrssd.value = Array.from(new Set([selSsd, selHdd]))
    })
    // CPU
    watch(cpuSelBrand, async (cpu: string) => {
      const response: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=cpu&brand=${cpu}`
      )
      const cpuSelModels: string[] = []
      for (let cpuData of response.data) {
        if (cpu === cpuData['Brand']) cpuSelModels.push(cpuData['Model'])
      }
      cpuModels.value = cpuSelModels
    })
    // GPU
    watch(gpuSelBrand, async (gpu: string) => {
      const response: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=gpu&brand=${gpu}`
      )
      const gpuSelModels: string[] = []
      for (let gpuData of response.data) {
        if (gpu === gpuData['Brand']) gpuSelModels.push(gpuData['Model'])
      }
      gpuModels.value = gpuSelModels
    })
    // ram
    watch(manyRam, async (num: string) => {
      watch(ramBrand, async (ram) => {
        const response: AxiosResponse = await axios.get(
          `https://api.recursionist.io/builder/computers?type=ram&brand=${ram}`
        )
        const ramSelModels: string[] = []
        for (let ramData of response.data) {
          const ramMod = ramData.Model
          const nums = parseInt(ramMod.slice(-6, ramMod.lemngth).replace(' ', '').slice(0, 1), 10)
          if (parseInt(num) === nums) ramSelModels.push(ramData.Model)
        }
        ramModels.value = ramSelModels
      })
    })
    //storage
    watch(selhddOrssdes, async (ssd: string | any) => {
      let str: string = ''
      if (ssd === 'SSD') str = 'ssd'
      if (ssd === 'HDD') str = 'hdd'
      const response: AxiosResponse = await axios.get(
        `https://api.recursionist.io/builder/computers?type=${str}`
      )
      let ssdList: string[] = [
        '58GB',
        '118GB',
        '128GB',
        '250GB',
        '256GB',
        '280GB',
        '400GB',
        '480GB',
        '500GB',
        '512GB',
        '800GB',
        '960GB',
        '1TB',
        '2TB',
        '4TB'
      ]
      let hddList: string[] = [
        '250GB',
        '300GB',
        '450GB',
        '500GB',
        '1TB',
        '1.5TB',
        '2TB',
        '3TB',
        '4TB',
        '5TB',
        '6TB',
        '8TB',
        '10TB',
        '12TB'
      ]
      if (response.data[0].Type === 'SSD') {
        storageCap.value = Array.from(new Set(ssdList))
      }
      if (response.data[0].Type === 'HDD') {
        storageCap.value = Array.from(new Set(hddList))
      }
      watch(storageCapes, async (storage: string) => {
        const stoBrands: string[] = []
        for (let manySto of response.data) {
          if (manySto.Model.split(' ').includes(storage)) {
            stoBrands.push(manySto.Brand)
          }
        }
        const sortedBrands: string[] = stoBrands
          .filter((ele, i) => stoBrands.indexOf(ele) === i)
          .sort()
        storageSelBrand.value = sortedBrands
      })
      watch(storageSelBrandes, async (brands) => {
        const stoModels: string[] = []
        const storage: string = storageCapes.value
        for (let manySto of response.data) {
          if (manySto.Model.split(' ').includes(storage) && manySto.Brand === brands)
            stoModels.push(manySto.Model)
        }
        storageSelModel.value = stoModels
      })
    })
    const addBtn = () => {
      cpuBrand.value = cpuSelBrand.value
      cpuModel.value = cpuResModel.value
      gpuBrand.value = gpuSelBrand.value
      gpuModel.value = gpuResModel.value
      ramBrandes.value = ramBrand.value
      ramModel.value = ramResModel.value
      reshddOrssd.value = selhddOrssdes.value
      resStorage.value = storageCapes.value
      resStoBrand.value = storageSelBrandes.value
      resStoModel.value = storageSelModeles.value
      const gaming: number = 0.6 + 0.25 + 0.025 + 0.025
      const working: number = 0.6 + 0.25 + 0.1 + 0.05
      const resRam: number = parseInt(
        ramResModel.value.slice(-4, ramResModel.value.length).replace('x', '').slice(0, -2),10);
      const res: number = 100 - parseInt(manyRam.value, 10) * resRam
      resGaming.value = Math.floor(res * gaming)
      resWorking.value = Math.floor(res * working)
      if (
        cpuBrand.value[0] !== undefined &&
        cpuModel.value[0] !== undefined &&
        gpuBrand.value[0] !== undefined &&
        gpuModel.value[0] !== undefined &&
        ramBrandes.value[0] !== undefined &&
        ramModel.value[0] !== undefined &&
        reshddOrssd.value[0] !== undefined &&
        resStorage.value[0] !== undefined &&
        resStoBrand.value[0] !== undefined &&
        resStoModel.value[0] !== undefined
      ) isAdded.value = true;
    }
    return {
      cpuBrands,
      cpuSelBrand,
      cpuModels,
      cpuResModel,
      gpuSelBrands,
      gpuSelBrand,
      gpuModels,
      gpuResModel,
      manyRam,
      manyRams,
      ramBrand,
      ramBrands,
      ramModels,
      ramResModel,
      selhddOrssd,
      selhddOrssdes,
      storageCap,
      storageCapes,
      storageSelBrand,
      storageSelBrandes,
      storageSelModel,
      storageSelModeles,
      isAdded,
      addBtn,
      cpuBrand,
      cpuModel,
      gpuBrand,
      gpuModel,
      ramBrandes,
      ramModel,
      reshddOrssd,
      resStorage,
      resStoBrand,
      resStoModel,
      resGaming,
      resWorking
    }
  }
})
</script>

<style scoped>
.titleDiv {
  background-color: blue;
}
.mainBody {
  margin-left: 30px;
}
.select {
  width: 10vw;
  margin-bottom: 15px;
}
.outerSpace {
  padding-left: 10px;
}
.innerSpace {
  margin-left: 10px;
}
.resSpace {
  padding-left: 20px;
}
</style>
