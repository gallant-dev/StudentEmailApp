<template>
  <div class="students">
    <h1>{{ title }}</h1>
    <div>
     <div class="my-1 row">
       <div class="col-6">
         <b-form-fieldset horizontal label="Rows per page" :label-cols="6">
           <b-form-select :options="[{text:5,value:5},{text:10,value:10},{text:15,value:15}]" v-model="perPage">
           </b-form-select>
         </b-form-fieldset>
       </div>
       <div class="col-6">
         <b-form-fieldset horizontal label="Filter" :label-cols="3">
           <b-form-input v-model="filter" placeholder="Type to Search"></b-form-input>
         </b-form-fieldset>
       </div>
     </div>

     <div class="justify-content-center my-1 row">
      <div class="col-6">
         <b-pagination size="md" :total-rows="items.length" :per-page="perPage" v-model="currentPage" />
      </div>
      <div class="col-6">
       <b-btn size="md" variant="primary" v-b-modal.emailEditor>Email Selected</b-btn>
      </div>
     </div>
     <b-table striped hover
              :items="items"
              :fields="fields"
              :current-page="currentPage"
              :per-page="perPage"
              :filter="filter"
     >
       <template slot="selected" scope="item">
         <b-form-checkbox v-model="item.value" value="true" unchecked-value="false">
         </b-form-checkbox>
       </template>
       <template slot="name" scope="item">
         {{item.value.first}} {{item.value.last}}
       </template>
       <template slot="contactName" scope="item">
         {{item.value.first}} {{item.value.last}}
       </template>
       <template slot="agreed" scope="item">
         {{item.value?'Yes':'No'}}
       </template>
     </b-table>
     <b-modal id="emailEditor" size="lg" min-height="600" title="Compose Email" @ok="submit" @shown="clearName">
       <form @submit.stop.prevent="submit">
         <b-form-input size="md" textarea v-model="emailContent"></b-form-input>
       </form>
     </b-modal>
    </div>
  </div>
</template>

<script>
export default {
  name: 'students',
  data () {
    return {
      title: 'List of Students',
      items: [
            {
              selected: false, agreed: true, name: { first: 'Dickerson', last: 'Macdonald' }, contactName: { first: 'Marge', last: 'Macdonald'}, contactEmail: 'mmacdonald@gmail.com'
            }, {
              selected: false, agreed: false, name: { first: 'Larsen', last: 'Shaw' }, contactName: { first: 'Steve', last: 'Shaw'}, contactEmail: 'sshaw@gmail.com'
            }, {
              selected: false, agreed: false, name: { first: 'Mitzi', last: 'Navarro' }, contactName: { first: 'Marco', last: 'Navarro'}, contactEmail: 'mnavarro@gmail.com'
            }, {
              selected: false, agreed: false, name: { first: 'Geneva', last: 'Wilson' }, contactName: { first: 'Philis', last: 'Wilson'}, contactEmail: 'pwilson@yahoo.com'
            }, {
              selected: false, agreed: true, name: { first: 'Jami', last: 'Carney' }, contactName: { first: 'Barbera', last: 'Carney'}, contactEmail: 'bcarney@hotmail.com'
            }, {
              selected: false, agreed: false, name: { first: 'Essie', last: 'Dunlap' }, contactName: { first: 'Roberto', last: 'Dunlap'}, contactEmail: 'rdunlap@gmail.com'
            }, {
              selected: false, agreed: true, name: { first: 'Mallory', last: 'Macdonald' }, contactName: { first: 'Marge', last: 'Macdonald'}, contactEmail: 'mmacdonald@gmail.com'
            },
          ],
          fields: {
      selected: {
        label: 'Selected',
        sortable: true
      },
      name: {
        label: 'Person Full name',
        sortable: true
      },
      contactName: {
        label: 'Parent Name',
        sortable: true
      },
      agreed: {
        label: 'Agreed',
        sortable: true
      },
      contactEmail: {
        label: 'Contact Email',
        sortable: true
      }
    },
    currentPage: 1,
    perPage: 5,
    filter: null,
    emailContent:`We would like to take your child on a school trip.
    Do you agree??
    http://something.com/`
  }
},
methods: {
  details(item) {
    alert(JSON.stringify(item));
  }
}
}
</script>

<style scoped>

</style>
