<script setup>
import TimelineEchart from './components/TimelineEchart.vue';
</script>

<template>
  <div class="common-layout">
    <el-container>
      <el-main>
        <el-row class="el-row" :gutter="12">
          <el-col :span="24">
            <el-card class="no-v-padding">
              <TimelineEchart />
            </el-card>
          </el-col>
        </el-row>
      </el-main>
    </el-container>
  </div>
</template>

<style scoped>
.no-v-padding {
  padding-right: 0;
  padding-left: 0;
}

.el-row {
  margin-bottom: 10px;
}
</style>
