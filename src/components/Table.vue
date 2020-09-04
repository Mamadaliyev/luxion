<template>
  <div class="table">
    <el-row class="add-header">
      <el-col :span="2" :offset="2">
        <el-button @click="handleClickAdd" type="primary" icon="el-icon-plus"
          >Добавить</el-button
        >
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="20" :offset="2">
        <el-table resizable="false" border :data="tableData">
          <el-table-column width="59" label="№" type="index"></el-table-column>
          <el-table-column
            width="180"
            label="Категория"
            prop="category"
          ></el-table-column>
          <el-table-column
            width="180"
            label="Подкатегория"
            prop="subCategory"
          ></el-table-column>
          <el-table-column width="180" label="Название" prop="name">
          </el-table-column>
          <el-table-column width="180" label="Тип" prop="type">
          </el-table-column>
          <el-table-column width="120" label="Цена покупки" prop="buyPrice">
          </el-table-column>
          <el-table-column width="120" label="Цена продажи" prop="sellPrice">
          </el-table-column>
          <el-table-column width="150" align="right">
            <template slot-scope="scope">
              <el-button
                type="warning"
                @click="handleEdit(scope.row.id)"
                icon="el-icon-edit"
              ></el-button>
              <el-button
                type="danger"
                @click="handleDelete(scope.row.id)"
                icon="el-icon-delete"
              ></el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-col>
    </el-row>

    <el-dialog :visible.sync="dialogVisible">
      <div class="edit-form">
        <el-form size="mini" label-width="120px" :model="formData">
          <el-form-item label="Категория">
            <el-select
              class="select-type"
              v-model="formData.category"
              placeholder=""
            >
              <el-option
                v-for="type in formData.types"
                :key="type.title"
                :label="type.title"
                :value="type.title"
              >
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Подкатегория">
            <el-select v-model="formData.itemOfSelected" placeholder="">
              <el-option
                v-for="type in formData.types"
                :key="type.title"
                :label="type.title"
                :value="type.title"
              ></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Название">
            <el-input required v-model="formData.name"></el-input>
          </el-form-item>
          <el-form-item label="Тип">
            <el-input required v-model="formData.type"></el-input>
          </el-form-item>
          <el-form-item label="Цена покупки">
            <el-input
              required
              type="number"
              v-model="formData.buyPrice"
            ></el-input>
          </el-form-item>
          <el-form-item label="Цена продажи">
            <el-input
              required
              type="number"
              v-model="formData.sellPrice"
            ></el-input>
          </el-form-item>
        </el-form>
        <div class="el-form-buttons">
          <el-button @click="handleDialogCancel">Отмена</el-button>
          <el-button v-if="editMode" @click="handleDialogUpdate" type="primary">
            Обновить
          </el-button>
          <el-button v-else @click="handleDialogAdd" type="primary">
            Добавить
          </el-button>
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  name: "Table",
  data() {
    return {
      dialogVisible: false,
      editMode: false,
      formData: {
        category: null,
        types: [{ title: "Category 1" }, { title: "Category 2" }],
        itemOfSelected: null,
        name: "",
        type: "",
        buyPrice: "",
        sellPrice: "",
      },
      tableData: [
        {
          category: "Type1",
          subCategory: "subcat1",
          name: "Name 1",
          type: "type 1",
          buyPrice: "2000",
          sellPrice: "2500",
          id: "12345",
        },
        {
          category: "Type2",
          subCategory: "subcat2",
          name: "Name 2",
          type: "type 2",
          buyPrice: "1000",
          sellPrice: "1500",
          id: "1525",
        },
        {
          category: "Type3",
          subCategory: "subcat3",
          name: "Name 3",
          type: "type 3",
          buyPrice: "3000",
          sellPrice: "3500",
          id: "5454",
        },
        {
          category: "Type4",
          subCategory: "subcat4",
          name: "Name 4",
          type: "type 4",
          buyPrice: "4000",
          sellPrice: "4500",
          id: "4545",
        },
      ],
    };
  },
  methods: {
    handleEdit(id) {
      this.editMode = true;
      this.dialogVisible = true;
      console.log("edit", id);
    },
    handleDelete(id) {
      console.log("delete", id);
    },
    handleDialogCancel() {
      this.dialogVisible = false;
    },
    handleDialogUpdate() {
      this.dialogVisible = false;
    },
    handleDialogAdd() {
      console.log(this.formData);
      const item = {
        category: this.formData.category,
        subCategory: this.formData.itemOfSelected,
        name: this.formData.name,
        type: this.formData.type,
        buyPrice: this.formData.buyPrice,
        sellPrice: this.formData.sellPrice,
        id: "6545",
      };
      this.tableData.push(item);
      this.dialogVisible = false;
    },
    handleClickAdd() {
      this.clearDialog();
      this.editMode = false;
      this.dialogVisible = true;
    },
    clearDialog() {
      this.formData = {
        category: null,
        types: [{ title: "Category 1" }, { title: "Category 2" }],
        itemOfSelected: null,
        name: "",
        type: "",
        buyPrice: "",
        sellPrice: "",
      };
    },
  },
};
</script>
<style lang="scss">
.table {
  margin-top: 50px;
  text-align: center;
  .add-header {
    margin-bottom: 20px;
  }
}
.edit-form {
  .el-form-buttons {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    margin-top: 50px;
  }
}
@media screen and (max-width: 700px) {
  .el-dialog {
    width: 95% !important;
  }
}
</style>
