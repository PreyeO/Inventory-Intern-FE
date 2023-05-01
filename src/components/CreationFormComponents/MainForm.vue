<template>
  <div>
    <div class="action_buttons">
      <h5>Inventory</h5>
      <ActionButton class="buttons" :product="product" />
    </div>
    <div class="flex creation_forms">
      <div>
        <q-form
          @submit.prevent="handleSubmit"
          class="q-pa-md shadow-2 details_form flex"
        >
          <label>Product Name</label>
          <LongInput
            :placeholder="'Canon EOS Rebel T7'"
            v-model="product.ProductName"
            type="text"
            required
          />
          <SelectInput
            :label="'Select Product Category'"
            value
            :options="ui.ProductCategory"
            v-model="product.ProductCategory"
          />

          <div class="flex product_pricing">
            <LongInput
              :placeholder="'Selling price'"
              type="number"
              class="price_input"
              v-model="product.sellingPrice"
            />
            <LongInput
              :placeholder="'Cost price'"
              type="number"
              class="price_input"
              v-model="product.costPrice"
            />
          </div>
          <LongInput
            :placeholder="'Quantity in Stock'"
            type="number"
            v-model="product.quantityInStock"
          />
          <SelectInput
            :label="'Order Type'"
            :options="ui.OrderType"
            v-model="product.OrderType"
          />
          <div class="flex form_discount">
            <div>
              <label class="q-mr-md">Discount</label>
            </div>
            <div class="form_discounts">
              <label class="q-mr-md">Add Discount</label>
            </div>
          </div>
          <div class="flex discount_values">
            <SelectInput
              :label="'Discount Type'"
              :options="ui.discountType"
              v-model="product.discountType"
              class="discount_input"
            />
            <LongInput
              :placeholder="'Discount Value'"
              v-model="product.discountValue"
              class="discount_input"
            />
          </div>
          <div class="flex expiry_date">
            <div>
              <label class="q-mr-md">Expiry Date</label>
            </div>
            <div>
              <label class="q-mr-md">Add Expiry Date</label>
            </div>
          </div>
          <LongInput type="date" v-model="product.expiryDate" />
          <div>
            <div>
              <label>Return Policy</label>
              <SelectInput
                :label="'Return Policy'"
                :options="ui.returnPolicy"
                v-model="product.returnPolicy"
              />
            </div>
          </div>
          <label>Date Added</label>
          <div class="flex time_date">
            <LongInput
              type="date"
              v-model="product.dateAdded"
              class="q-mr-md form_date_time"
            />
            <LongInput
              type="time"
              v-model="product.timeAdded"
              class="q-mr-md form_date_time"
            />
          </div>
        </q-form>
      </div>
      <q-form class="q-pa-md shadow-2 q-mr-lg image_form">
        <div>
          <UploadFile v-model="product.imageUrl" style="height: 20rem" />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
import LongInput from "./LongInput.vue";
import SelectInput from "./SelectInput.vue";
// import TextEditor from "./TextEditor.vue";
import UploadFile from "./UploadFile.vue";
import ActionButton from "./ActionButton.vue";
import { mapActions } from "vuex";

export default {
  name: "MainForm",
  components: { LongInput, SelectInput, UploadFile, ActionButton },
  props: {
    label: {
      type: String,
      required: true,
    },
    options: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      ui: {
        ProductCategory: ["gadget", "automobile", "electronics", "groceries"],
        OrderType: ["return", "purchase", "in stock", "out of stock"],
        discountType: ["fixed", "percentage"],
        returnPolicy: ["yes", "no"],
      },
      product: {
        ProductName: "",
        ProductCategory: "",
        OrderType: "",
        sellingPrice: "",
        costPrice: "",
        quantityInStock: "",
        discountType: "",
        discountValue: "",
        returnPolicy: "",
        dateAdded: "",
        timeAdded: "",
        imageUrl: "",
        status: ["Draft", "Published"],
        expiryDate: "",
      },
    };
  },
  methods: {
    ...mapActions("inventory", ["publishProduct"]),
  },
};
</script>
<style scoped>
.creation_forms {
  gap: 3rem;
  flex-wrap: wrap;
  min-width: 100%;
}
.details_form {
  min-width: 100%;
  flex-wrap: wrap;
  flex-direction: column;
  margin-left: 2rem;
}
.image_form {
  min-width: 30%;
}
.product_pricing {
  flex-wrap: wrap;
  justify-content: space-between;
}
.price_input {
  width: 45%;
}
.form_discount {
  justify-content: space-between;
}
.discount_values {
  justify-content: space-between;
}
.discount_input {
  width: 45%;
}
.expiry_date {
  justify-content: space-between;
}
.return_policy {
  justify-content: space-between;
}
.time_date {
  justify-content: space-between;
}
.form_date_time {
  width: 45%;
}
.action_buttons {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
h5 {
  padding-left: 5rem;
  padding-top: 2rem;
}

@media (max-width: 760px) {
  .details_form {
    margin-left: 0;
  }
  .creation_forms {
    justify-content: center;
    padding: 1rem;
  }
  .image_form {
    min-width: 100%;
    margin: 0 auto;
  }
  .buttons {
    min-width: 1rem;
    margin-top: 0;
  }
}

@media (min-width: 770px) {
  .image_form {
    min-width: 20%;
    margin: 0 auto;
  }
  .details_form {
    min-width: 50%;
  }
  .creation_forms {
    gap: 1rem;
  }
}
</style>
