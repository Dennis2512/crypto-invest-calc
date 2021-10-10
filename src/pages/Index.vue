<template>
  <q-page class="JetBrainsMonoFont">
    <div class="q-pa-md">
      <div class="text-h2">
        <div class="text-accent">Dashboard</div>
        <!-- <div class="text-accent">Currency Overview</div> -->
      </div>
    </div>
    <q-input
      class="q-px-md"
      square
      filled
      placeholder="Search..."
      v-model="filter"
    >
      <template v-slot:prepend>
        <!-- v-slot:append would set icons to the right-->
        <q-icon v-if="filter === ''" name="search" />
        <q-icon
          v-else
          name="clear"
          class="cursor-pointer"
          @click="filter = ''"
        />
      </template>
    </q-input>
    <div class="q-pa-md">
      <q-table
        title="Currency Overview"
        :grid="$q.screen.xs"
        table-header-class="bg-grey-2"
        class="test"
        no-data-label="No data available. Please use the searchbar above to find matching currencies."
        :data="data"
        :columns="columns"
        :filter="filter"
        row-key="name"
      >
        <template v-slot:header="props">
          <q-tr :props="props">
            <q-th
              v-for="col in props.cols"
              :key="col.name"
              :props="props"
              class="text-weight-bold bg-grey-2"
              style="font-family: JetBrainsMono"
            >
              {{ col.label }}
            </q-th>
          </q-tr>
        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script lang="ts">
export default {
  data() {
    return {
      filter: '',
      columns: [
        {
          name: 'name',
          required: true,
          label: 'Name',
          align: 'left',
          // field: row => row.name,
          // format: val => `${val}`,
          field: (row: { name: string }) => row.name,
          format: (val: string) => `${val}`,
          classes: 'bg-grey-2 ellipsis',
          style: 'max-width: 100px',
          headerClasses: 'bg-grey-4',
          // headerClasses: 'bg-primary text-white',
          sortable: true
        },
        {
          name: 'shorty',
          align: 'center',
          label: 'Abbreviation',
          field: 'shorty',
          sortable: true
        },
        {
          name: 'price',
          align: 'center',
          label: 'Price (EUR)',
          field: 'price',
          sortable: true
        },
        {
          name: 'inv',
          align: 'center',
          label: 'Investment (EUR)',
          field: 'inv',
          // classes: 'bg-red-2',
          classes: 'text-red-6',
          // headerClasses: 'bg-red-3',
          sortable: true
        },
        {
          name: 'roi',
          align: 'center',
          label: 'Return on Investment (EUR)',
          field: 'roi',
          // classes: 'bg-green-2',
          classes: 'text-green-6',
          // headerClasses: 'bg-green-3',
          sortable: true
        }
      ],
      data: [
        {
          name: 'BitcoinoinoinoinDennisBenediktSahra',
          shorty: 'BTC',
          price: 45230.89,
          inv: 10000,
          roi: 6952.37
        },
        {
          name: 'Ethereum',
          shorty: 'ETH',
          price: 2360.65,
          inv: 1000.05,
          roi: 800.64
        },
        {
          name: 'Dogecoin',
          shorty: 'DOGE',
          price: 0.00016,
          inv: 10,
          roi: 500
        }
      ]
    };
  }
};
</script>

<style lang="sass" scoped>
.test
  tr th
    font-family: JetBrainsMonoFont,
    font-weight: 700
</style>
