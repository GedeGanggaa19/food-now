<template>
  <div class="homepage container">
    <div class="utama">
      <div class="content">
        <!-- Choose Your Pizza -->
        <h1 class="title">Choose Your Pizza</h1>
        <div class="pizza-list">
          <div
            v-for="pizza in pizzas"
            :key="pizza.id"
            class="pizza-card"
            :class="{ highlighted: pizza.discount.is_active, selected: selectedPizza === pizza }"
            @click="selectPizza(pizza)"
          >
            <img
              :src="getImagePath(pizza.name, 'pizza')"
              :alt="pizza.name"
              class="pizza-image"
            />
            <div class="pizza-details">
              <h3>{{ pizza.name }}</h3>
              <p>
                <span v-if="pizza.discount.is_active" class="discounted-price">
                  ${{ pizza.discount.final_price.toFixed(2) }}
                </span>
                <span v-if="pizza.discount.is_active" class="original-price">
                  ${{ pizza.price.toFixed(2) }}
                </span>
                <span v-else>
                  ${{ pizza.price.toFixed(2) }}
                </span>
              </p>
              <img
                v-if="pizza.discount.is_active"
                class="offer-badge"
                src="/src/assets/images/ribbon.svg"
                alt="Offer Badge"
              />
            </div>
          </div>
        </div>

        <!-- Custom Pizza -->
        <h1 class="title">Custom Pizza</h1>

        <!-- Size Options -->
        <div class="toppings-section">
          <h4>Size</h4>
          <div class="size-options">
            <label v-for="size in sizes" :key="size.id">
              <input
                type="radio"
                class="styled-radio"
                name="size"
                :value="size"
                v-model="selectedSize"
              />
              {{ size.name }}
              <span v-if="size.extra_price > 0">(+${{ size.extra_price }})</span>
            </label>
          </div>
        </div>

        <!-- Topping Options -->
        <div class="toppings-section">
          <h4>Toppings</h4>
          <div class="toppings-options mt-5">
            <label
              v-for="topping in toppings"
              :key="topping.id"
              class="styled-label"
              :class="{ 'disabled-label': !isToppingEnabled(topping) }"
            >
              <input
                type="checkbox"
                :value="topping"
                v-model="selectedToppings"
                class="styled-checkbox"
                :disabled="!isToppingEnabled(topping)"
              />
              <span class="topping-text py-2">{{ topping.name }}</span>
            </label>
          </div>
        </div>
      </div>

      <!-- Payment Summary -->
      <div class="payment-summary sticky-top top-5">
        <h2>Payment Summary</h2>
        <ul class="summary-list">
          <li>
            Pizza: {{ selectedPizza?.name || "-" }}
            <span>${{ selectedPizzaPrice.toFixed(2) }}</span>
          </li>
          <li>
            Pizza Size: {{ selectedSize?.name || "-" }}
            <span>${{ sizePrice.toFixed(2) }}</span>
          </li>
          <li v-for="(topping, index) in selectedToppings" :key="index">
            {{ topping.name }} <span>${{ topping.price.toFixed(2) }}</span>
          </li>
        </ul>
        <hr />
        <div class="total">
          <span>Total Price</span>
          <span class="total-price">${{ totalPrice.toFixed(2) }}</span>
        </div>
        <button class="order-button" @click="orderNow">Order Now</button>
      </div>
    </div>

    <!-- Modal Pop-Up -->
    <div v-if="showPopup" class="modal-overlay" @click.self="closePopup">
      <div class="modal-content align-items-center">
        <img src="@/assets/images/order/order.gif" alt="Order Success" width="200" />
        <h2>Order Success</h2>
        <p>Thank you, we have received your order successfully.</p>
        <button class="close-button" style="width: 100%;" @click="closePopup">Close</button>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, computed } from "vue";
import pizzaList from "@/assets/json/pizza-list.json";
import sizeList from "@/assets/json/size-list.json";
import toppingList from "@/assets/json/topping-list.json";

// State
const pizzas = ref(pizzaList.data);
const sizes = ref(sizeList.data);
const toppings = ref(toppingList.data);
const selectedPizza = ref(null);
const selectedSize = ref(null);
const selectedToppings = ref([]);
const showPopup = ref(false);

// Computed Properties
const selectedPizzaPrice = computed(() =>
  selectedPizza.value?.discount.is_active
    ? selectedPizza.value.discount.final_price
    : selectedPizza.value?.price || 0
);

const sizePrice = computed(() => selectedSize.value?.extra_price || 0);

const toppingPrice = computed(() =>
  selectedToppings.value.reduce((sum, topping) => sum + topping.price, 0)
);

const totalPrice = computed(
  () => selectedPizzaPrice.value + sizePrice.value + toppingPrice.value
);

// Methods
function getImagePath(name, type = "pizza") {
  const folder = type === "pizza" ? "pizza" : "";
  return new URL(
    `/src/assets/images/${folder}/${name.replace(/\s/g, "-")}.png`,
    import.meta.url
  ).href;
}

function selectPizza(pizza) {
  selectedPizza.value = selectedPizza.value === pizza ? null : pizza;
  selectedToppings.value = [];
}

function isToppingEnabled(topping) {
  return selectedPizza.value?.toppings.includes(topping.id) || false;
}

function orderNow() {
  if (!selectedPizza.value) {
    alert("Please select a pizza to order!");
    return;
  }
  showPopup.value = true;
}

function closePopup() {
  showPopup.value = false;
  window.location.reload();
}
</script>


<style scoped>

/* Umum */
.homepage {
  padding: 20px;
}

.title {
  margin-top: 70px;
  font-size: 2em;
  color: #f76c35;
  margin-bottom: 20px;
  text-align: left;
}

.utama {
  display: flex;

}

.content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 20px;
}

/* Choose Your Pizza */
.pizza-list {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.pizza-card {
  background-color: gray;
  display: flex;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: white;
  font-weight: bold;
  position: relative;
  text-align: center;
  transition: transform 0.3s, background-color 0.3s;
  align-items: center;
  text-align: left;
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.1);
}

.pizza-card:hover {
  transform: translateY(-10px);
  background-color: rgba(253, 159, 82, 0.701);
}

.pizza-card.selected {
  background-color: #f76c35;
  color: white;
  transition: background-color 0.3s ease-in-out;
}

.pizza-image {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-right: 15px;
  transition: transform 0.3s ease-in-out;
}

.pizza-card:hover .pizza-image {
  transform: rotate(50deg);
}

.pizza-details h3 {
  margin: 10px 0;
  font-size: 1.2em;
}

.original-price {
  text-decoration: line-through;
  color: gray;
  margin-left: 5px;
}

.offer-badge {
  position: absolute;
  top: 0;
  right: 0;
  width: 100px;
  height: auto;
  transform-origin: top right;
  z-index: 10;
}

/* Custom Pizza */
.size-options {
  display: flex;
  gap: 25px;
  margin-top: 10px;
}

.toppings-section h4 {
  margin-bottom: 10px;
  font-size: 1.2em;
  color: #333;
  text-align: left;
}

.toppings-options {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  margin-top: 10px;
}

.styled-label {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 3px solid #ddd;
  width: 15%;
  border-radius: 25px;
  background-color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 1em;
  color: #333;
}

.styled-label:hover {
  border-color: #f76c35;
  color: #f76c35;
}

.styled-checkbox {
  display: none;
}

.topping-text {
  font-size: 0.9em;
  font-weight: bold;
}

.styled-checkbox:checked {
  border-color: #f76c35;
}

.styled-checkbox:checked + .topping-text {
  background-color: rgba(253, 159, 82, 0.701);
  border-radius: 25px;
  width: 100%;
  color: white;
  text-align: center;
}

/* Payment Summary */
.payment-summary {
  width: 450px;
  height: fit-content;
  padding: 20px;
  margin-left: 20px;
  margin-top: 90px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.1);
}

.payment-summary h2 {
  font-size: 1.5em;
  color: #f76c35;
  margin-bottom: 15px;
}

.summary-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.summary-list li {
  display: flex;
  justify-content: space-between;
  margin: 5px 0;
  font-size: 1em;
  color: #333;
}

.total {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  font-size: 1.2em;
  margin: 15px 0;
}

.order-button {
  width: 100%;
  padding: 10px 20px;
  background-color: #f76c35;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
  font-size: 1em;
}

.order-button:hover {
  background-color: #d95e28;
}

.disabled-label {
  opacity: 0.5;
  pointer-events: none;
}

.size-options {
  display: flex;
  gap: 25px;
  margin-top: 10px;
}

.styled-radio {
  appearance: none; 
  width: 20px;
  height: 20px;
  margin-bottom: -3px;
  text-align: center;
  border: 2px solid #ccc;
  border-radius: 50%; 
  cursor: pointer;
  position: relative;
  transition: all 0.3s ease;
}

.styled-radio:checked {
  border-color: #f76c35; 
  background-color: #f76c35; 
}

.styled-radio:checked::after {
  content: '';
  width: 10px;
  height: 10px;
  border-radius: 50%; 
  background-color: white; 
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); 
}

/* Modal Overlay */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

.close-button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #f76c35;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
}

.close-button:hover {
  background-color: #d95e28;
}

/* Responsif untuk layar kecil */
@media (max-width: 768px) {
  .utama {
    flex-direction: column;
    align-items: center;
  }

  .content {
    width: 100%;
    text-align: center;
  }

  .pizza-image {
    width: 80px;
    height: 80px;
    margin-bottom: 10px;
  }

  .payment-summary {
    width: 100%;
    margin-left: 0;
    margin-top: 20px;
  }

  .size-options,
  .toppings-options {
    justify-content: center;
  }

  .styled-label {
    width: 30%;
  }
}

/* Responsif untuk layar sangat kecil (ponsel) */
@media (max-width: 480px) {
  .pizza-card {
    padding: 10px;
    flex-direction: column;
  }

  .pizza-image {
    width: 60px;
    height: 60px;
  }

  .pizza-details h3 {
    font-size: 1em;
  }

  .styled-label {
    font-size: 0.8em;
    width: 45%;
  }

  .order-button,
  .close-button {
    font-size: 0.9em;
    padding: 8px;
  }
}

</style>
