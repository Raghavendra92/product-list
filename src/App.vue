<template>
  <div class="app-container">
    <!-- <PageHeader /> -->
    <ProductTable />
  </div>
</template>

<script>
import ProductTable from './components/ProductTable.vue';
// import PageHeader from './components/PageHeader.vue';

export default {
  name: 'App',
  components: {
    ProductTable,
    // PageHeader
  }
}
</script>

<style lang="scss">
  @media(min-width: 768px){
    .app-container {
      margin: 40px;
    }
    table {
      gap: 0px;
      border-radius: 8px 0px 0px 0px;
      border: 1px solid #E4E4EF;
      opacity: 0px;
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      background-color: white;
      border-radius: 10px;
      overflow: hidden;
    }

        thead {
      tr {
        background-color: #f8f9fa;
        text-align: center;
      }

      th {
        padding: 15px;
        font-weight: 600;
        border-bottom: 1px solid #E4E4EF;
        font-family: 'Nunito Sans', sans-serif;
      }
    }

    tbody {
      td {
        border-bottom: 1px solid #e5e7eb;
      }

      td {
        //styleName: Body 1;
        font-family: 'Nunito Sans', sans-serif;
        font-size: 14px;
        font-weight: 400;
        line-height: 20px;
        color: #1A1A1A;

        padding: 15px;
        vertical-align: middle;
        text-align: center;

        &:first-child {
          border-left: 1px solid #e5e7eb;
        }

        &:last-child {
          border-right: 1px solid #e5e7eb;
        }

        small {
          color: #6c757d;
        }
      }
    }
  }

@media (max-width: 768px) {
  .app-container {
    margin: 20px;
  }
  table {
    display: block;
    overflow-x: auto;
  }

  .header {
    .hamburger {
      display: block;
    }

    .menu {
      display: none;
    }
  }
}

  .status-cell{
    padding: 4px 24px 4px 24px;
    border-radius: 12px;
    opacity: 0px;
    font-family: 'Nunito Sans', sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 20px;
    text-align: center;

  }

  .available{
    background: #EDEDFE;
    color: #605DEC;
  }

  .no-stock {
    background: #FFF4E4;
  }

.product-name {
  text-align: left;
}

.price {
  text-align: right
}

</style>
