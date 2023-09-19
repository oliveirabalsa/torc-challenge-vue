<template>
  <v-app>
    <v-container fluid fill-height>
      <v-row justify="center" align="center">
        <v-col cols="12">
          <v-card>
            <v-card-title class="title">Product Table</v-card-title>
            <v-card-text>
              <table>
                <thead>
                  <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Stock</th>
                    <th>Categories</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item, index) in sales" :key="item.productId">
                    <td>{{ item.productId }}</td>
                    <td>{{ item.productName }}</td>
                    <td>{{ item.productStock }}</td>
                    <td>{{ item.productCategories.join(', ') }}</td>
                  </tr>
                </tbody>
              </table>
            </v-card-text>
            <v-card-actions>
              <v-form class="form">
                <v-text-field v-model="form.productName" label="Product Name"></v-text-field>
                <v-text-field v-model="form.productStock" label="Product Stock" type="number"></v-text-field>
                <v-select v-model="form.productCategories" :items="categoryOptions" label="Product Categories" multiple></v-select>
                <v-btn class="btn" @click="updateTable" color="primary" variant="elevated">Submit</v-btn>
              </v-form>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script lang="ts">

import products from './data/products.json';

export default {
  name: "App",
  data: () => ({
    form: {
      productId: "",
      productName: "",
      productStock: 0,
      productCategories: [],
    },
    sales: products,
    categoryOptions: ["First", "Second", "Third"],
  }),
  methods: {
    updateTable() {
      const newProductId = Date.now().toString();
      this.form.productId = newProductId;
      this.sales.push({
        ...this.form,
        productCategories: [...this.form.productCategories],
      });
      this.resetForm();
    },
    resetForm() {
      this.form.productId = "";
      this.form.productName = "";
      this.form.productStock = 0;
      this.form.productCategories = [];
    },
  },
};
</script>

<style>

.title {
  text-align: center;
}

table {
  width: 100%;
  max-width: 70vh;
  margin: auto;
}

th {
  text-align: left;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  margin: 3rem auto;
  max-width: 80vh;

}

.btn {
  width: 30%;
  margin-left: auto;
}
</style>
