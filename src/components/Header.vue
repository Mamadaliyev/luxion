<template>
  <div class="header">
    <el-row :gutter="20">
      <el-col :lg="4" :md="8">
        <el-select
          class="select-type"
          v-model="selected"
          placeholder="Категория"
        >
          <el-option
            v-for="type in types"
            :key="type.id"
            :label="type.title"
            :value="type.id"
          >
          </el-option>
        </el-select>
      </el-col>
      <el-col :span="4">
        <el-select v-model="itemOfSelected" placeholder="Подкатегория">
          <el-option
            v-for="type in types"
            :key="type.id"
            :label="type.title"
            :value="type.id"
          ></el-option>
        </el-select>
      </el-col>
      <el-col :span="3">
        <el-input v-model="name" placeholder="Название"></el-input>
      </el-col>
      <el-col :span="3">
        <el-input v-model="type2" placeholder="Тип"></el-input>
      </el-col>
      <el-col :span="3">
        <el-input v-model="buyPrice" placeholder="Цена покупки"></el-input>
      </el-col>
      <el-col :span="3">
        <el-input v-model="sellPrice" placeholder="Цена продажи"></el-input>
      </el-col>
      <el-col :span="2" :offset="1">
        <el-button type="primary" icon="el-icon-plus">Добавить</el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      selected: null,
      types: [
        { title: "Type 1", id: "123456" },
        { title: "Type 2", id: "123457" },
      ],
      itemOfSelected: null,
      name: "",
      type2: "",
      buyPrice: "",
      sellPrice: "",
    };
  },
  computed: {},
};
</script>

<style scoped lang="scss">
.header {
}
</style>
