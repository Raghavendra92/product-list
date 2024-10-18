<template>
  <div class="modal-overlay">
    <div class="modal-content">
      <header class="modal-header">
            <h2>{{ product.product }}</h2>
            <img src="@/assets/x.svg" @click="$emit('close')" />
      </header>
      <section class="modal-body">
        <img :src="product.image || placeholder" class="product-image" alt="Product Image" />
            <div class="product-details">
                <p>Key Features</p>
                <ul>
                    <li>Serial: {{ product.serial }}</li>
                    <li>Price: {{ product.total }}</li>
                    <li>Quantity: {{ product.quantity }}</li>
                </ul>
          </div>
      </section>
        <footer class="modal-footer">
          <button class="close-modal-button" @click="$emit('close')">Close</button>
        </footer>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product'],
  data() {
    return {
      placeholder: 'https://via.placeholder.com/150?text=No+Image',
    };
  },
};
</script>

<style scoped>
/* Modal overlay */

.modal-overlay {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

@media (max-width: 768px){
    .modal-overlay {
          top: 100px;
    }
}

@media (min-width: 768px){
    .modal-overlay {
          top: 0;
    }
}

/* Modal content */
.modal-content {
    font-family: 'Nunito Sans', sans-serif;
    background-color: white;
    padding: 40px;
    border-radius: 8px;
    max-width: 600px;
    width: 100%;
    position: relative;
}

@media (max-width: 768px) {
    .modal-header {
        margin-left: 20px;
        margin-right: 10px;
    }
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-header h2 {
  margin: 0;
}

.close-button {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

@media (min-width: 768px) {
    .modal-body {
        display: flex;
        margin-top: 40px;
    }
}

@media (max-width: 768px) {
    .modal-body {
        display: flex;
        flex-direction: column;
        text-align: center;
        margin: 0px 40px;
    }

    .product-details {
        text-align: left;
    }

    .modal-footer {
        margin: 10px;
    }

    .close-modal-button {
        width: 100%;
        font-family: 'Nunito Sans', sans-serif;
        padding: 16px 20px;
    }
}

.product-image {
  max-width: 300px;
  margin-right: 40px;
}

.product-details h3 {
  margin-top: 0;
}

.product-details ul {
  padding-left: 20px;
  line-height: 30px;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}

.close-modal-button {
  background-color: #f1f1f1;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 4px;
}

.product-image {
    height: 300px;
    width: 300px;
}

@media screen and (max-width: 768px) {
  .modal-content {
    width: 100%;
    height: 100%;
    max-width: none;
    max-height: none;
    border-radius: 0;
    padding: 20px;
  }

  .modal-header {
    padding-bottom: 10px;
  }

  .modal-footer {
    padding-bottom: 20px;
  }
}
</style>
