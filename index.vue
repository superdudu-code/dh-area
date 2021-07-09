<template>
  <div>
    <dh-area
      :province="form.province"
      :city="form.city"
      :area="form.district"
      :province-code="form.province_code"
      :city-code="form.city_code"
      :area-code="form.district_code"
      @change="handleAreaChange($event, form)"
    />
  </div>
</template>

<script>
  import DhArea from '@/components/DhArea'
  export default {
    name: 'index',
    components: { DhArea },
    data() {
      return {
        form: {}
      }
    },
    methods: {
      // 地点选择器
      handleAreaChange(area, obj) {
        this.$set(obj, 'province', area[0].label)
        this.$set(obj, 'province_code', area[0].value)
        this.$set(obj, 'city', area[1].label)
        this.$set(obj, 'city_code', area[1].value)
        this.$set(obj, 'district', area[2].label)
        this.$set(obj, 'district_code', area[2].value)
      }
    }
  }
</script>
<style scoped>
  
</style>