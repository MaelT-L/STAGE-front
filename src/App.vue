<template>
  <div id="app" class="container-fluid">
    <div class="row titre">
      <img src="./assets/OIP.jpg" alt="Logo Abes" class="logo col-2">
      <h1 class="col-10 mt-5">Hello-Abes</h1>
    </div>
    <div class="row justify-content-center">
      <div class="col-8 table-responsive">
        <table class="table table-bordered table-striped caption-top">
          <caption>Liste des applications</caption>
          <thead>
            <tr>
              <th>Nom</th>
              <th>Port</th>
              <th>Machine/ Serveur</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="container in containers" :key="container.id">
              <td>{{ container.name }}</td>
              <td>{{ container.port }}</td>
              <td>{{ container.machine }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import 'bootstrap'; 
import 'bootstrap/dist/css/bootstrap.min.css';
import '../style.css';

export default {
  data() {
    return {
      containers: [],
    };
  },
  created() {
    this.fetchContainers();
  },
  methods: {
    async fetchContainers() {
      try {
        const response = await axios.get('http://localhost:8081/container/getAll');
        this.containers = response.data;
        console.log(response.data);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
  },
};
</script>
