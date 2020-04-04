<template>
  <div>
    <Navbar />
    <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      History Transaction
    </p>
    <a href="#" class="card-header-icon" aria-label="more options">
      <span class="icon">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
    </a>
  </header>
  <div class="card-content">
    <div class="content">
      <table class="table is-hoverable">
        <thead>
          <tr>
            <th>ID Transaksi</th>
            <th>Waktu Transaksi</th>
            <th>Buku Yang Dipinjam</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th>1</th>
            <td><a href="https://en.wikipedia.org/wiki/Leicester_City_F.C." title="Leicester City F.C.">Leicester City</a> <strong>(C)</strong>
            </td>
            <td>81</td>
            <td class="buttons are-small">
              <button class="button is-info">Detail</button>
              <button class="button is-danger">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
  name: 'History',
  components: {
    Navbar,
  },
  data() {
    return {
      name: null,
    };
  },
  // methods: {

  // }
};
</script>
<style scoped>
  .card{
    margin: 0 10px;
  }
  button{
    margin: 0 5px;
  }
</style>
