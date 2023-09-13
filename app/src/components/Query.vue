<script>

import Modal from './Modal.vue'

import config from '../lib/config';

import {
  getPubMedResultsforOrganism
} from '../lib/api';

import { 
  capitalize
} from '../lib/helper';


export default {
  data() {

    return {
      query: '',           // input query state
      isLoading: false,    // loading state
      showResults: false,  // result state

      results: [],         // result array

      modal: {             // modal state
        show: false,
        title: '',
        data: ''
      }
    }
  },


  methods: {
    capitalize,

    // triggers request, when Query button is clicked
    search: function () {
      this.loadTestData();
      this.showResults = true;
    },

    // Test request, which also triggers loading indicator
    async loadTestData () {
      this.isLoading = true;
      this.results = await getPubMedResultsforOrganism('Human', this.query); // async pattern to avoid callback
      this.isLoading = false;
    },

    // is triggered when input is changed
    hideResults: function () {
      this.showResults = false;
    },

    showModal: function(title, data) {
      this.modal.title = title;
      this.modal.data = data;
      this.modal.show = true;
    }

  },

  components: {
    Modal
  }
};

</script>

<template>
  <!-- QUERY -->
  <section class="query">
    <h2>Query</h2>
    <form class="form" @submit.prevent="search()">
      <div class="form__group">
        <label for="gene" class="form__label query-label">Gene</label>
        <input 
          type="text" 
          name="gene" 
          v-model="query" 
          class="form__control query-input" 
          placeholder="Enter query" 
          @keyup="hideResults" />
        <span class="form__help-text">Enter gene name</span>
      </div>

      <input type="submit" value="Search" />
      
    </form>

    <br />
    <input type="submit" value="Modal Demo" @click="showModal('Title', 'Content')"/>
  </section>

  <section class="result-table" v-if="showResults">
    <h2>Results</h2>

    <!-- LOADING INDICATOR -->
    <span class="results-loading" v-if="isLoading"><div class="loading"></div></span>

    <!-- RESULT TABLE -->
    <table v-if="results.length > 0">
      <tr>
        <th>PMID</th>
        <th>Year</th>
        <th>Titel</th>
        <th>Type</th>
      </tr>
      <tr v-for="pub in results">
        <td>{{ pub.pmId }}</td>
        <td>{{ pub.Year }}</td>
        <td><a :href="pub.link" class="link--external" target="_new">{{ pub.title }}</a></td>
        <td>{{ pub.PublicationType }}</td>
      </tr>
    </table>
  </section>

  <!-- MODAL -->
  <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="modal.show" @close="modal.show = false">
      <template #body>
        <div>
          <h3>{{ modal.title }}</h3>
          <p>{{  modal.data }}</p>
        </div>
      </template>
    </modal>
  </Teleport>
</template>

<style lang="scss">

/* External links with indicator */
.link--external {
  background-image: url('/icons/external.svg');
  background-repeat: no-repeat;
  background-size: 0.8rem;
  background-position: right center;
  padding-right: 1em; 
  text-decoration-color: var(--primary7);
}

table {
  border-collapse: collapse;

  th, td {
  padding: 3px 10px;
  border: 1px solid var(--primary12);
}

  th, td.source, td.source a {
    font-weight: bold;
  }
}

.truncate {
  max-width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.query {
  padding: var(--space-6);
  background-color: var(--primary1);
  border-radius: 8px;

  --button-bg-color: var(--accent);
  --button-text-color: var(--white);

  h2 {
    margin-top: 0;
  }
}

.result-table {
  padding: var(--space-6);
  background-color: var(--primary1);
  border-radius: 8px;
  margin-top: 1em;
}

.loading {
  background-image: url('/icons/loading.svg');
  background-repeat: no-repeat;
  width: 1em;
  height: 1em;
  animation: rotation 2s infinite linear;
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}
</style>
