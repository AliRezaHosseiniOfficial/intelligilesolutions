<template>
  <section>
    <!-- title section -->
    <div class="container-full py-4">
      <p class="PageTitle">Comments</p>
    </div>
    <div class="container-full mt-4 px-4 TableBkg">
      <div class="d-flex justify-content-between pt-5 px-3">
        <!-- pagination -->
        <AdminPagination/>
        <!-- end pagination -->
        <!-- sort section -->
        <div class="d-flex align-items-center">
          <p class="sort">Sort</p>
          <p class="SortStatus px-2">Last Opened</p>
        </div>
        <!-- end sort section -->
      </div>
      <!-- table section -->
      <div class="container-full px-3">
        <table class="table align-middle mb-0 bg-white">
          <thead class="bg-light">
          <tr>
            <th>#</th>
            <th>Customer</th>
            <th>Product</th>
            <th>Date</th>
            <th>Time</th>
            <th>Score</th>
            <th>Comments</th>
            <th></th>
          </tr>
          </thead>
          <tbody>
          <tr>
            <td>
              <p>1</p>
            </td>
            <td>
              <p>Jack Dorsi</p>
            </td>
            <td>
              <p>Sella body butter</p>
            </td>
            <td>
              <p>September30,2022</p>
            </td>
            <td>
              <p>at 10:56 am</p>
            </td>
            <td>
              <i class="bi bi-star-fill starbi"></i>
              <i class="bi bi-star-fill starbi"></i>
              <i class="bi bi-star-fill starbi"></i>
              <i class="bi bi-star starbi"></i>
              <i class="bi bi-star starbi"></i>
            </td>
            <td style="width: 20%;">
              <p>
                I really had to prep my face to make it super hydrated.
                I found the coverage better with a Overall,
                it has good coverage
              </p>
            </td>
            <td>
              <button type="button" class="mx-2 DetailBtn btn btn-sm">
                <i class="CheckIcon bi bi-check2"></i>
              </button>
              <button type="button" class="DetailBtn btn btn-sm">
                <i class="CancelIcon bi bi-x-lg"></i>
              </button>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
import AdminPagination from "@/components/AdminPagination";
export default {
  name: "admin",
  layout: 'admin',
  components: {AdminPagination},
}
</script>

<style scoped>

.PageTitle {
  font-family: 'open sans', sans-serif;
  font-size: 16pt;
  color: #43425d;
  font-weight: 600;
}

.starbi {
  color: #ed8a19;
}

.CheckIcon {
  color: #fff;
  font-size: 16pt;
}

.CancelIcon {
  color: #000;
  font-size: 16pt;
}

.DetailBtn {
  background-color: #e99d7b;
  color: #231942;
  font-family: 'Source Sans Pro', sans-serif;
  padding: 0px 2px !important;
  text-transform: capitalize;
  border-radius: 8px;
  box-shadow: none;
}

.DetailBtn:focus {
  box-shadow: none;
}

th {
  background-color: #f5f6fa;
  font-family: "Source Sans Pro", sans-serif;
  font-weight: 400;
  font-size: 10pt;
  color: #212529;
  padding: 10px 15px;
  border-bottom: 0;
}

td {
  color: black;
  font-weight: 400;
  font-family: "Source Sans Pro", sans-serif;
  vertical-align: top;
}

p {
  margin-bottom: 0;
}

.DetailBtn {
  background-color: #e99d7b;
  color: #231942;
  font-family: "Source Sans Pro", sans-serif;
  font-size: 10pt;
  padding: 5px 25px;
  text-transform: capitalize;
}

.DetailBtn:focus {
  box-shadow: none;
}

.page-link {
  color: #4d4f5c;
  padding: 8px 15px;
}

.page-link:focus {
  background-color: #055452;
  color: #fff;
  box-shadow: none;
}

.SortStatus {
  color: #828282;
  font-family: "Open Sans";
  font-size: 10pt;
  font-weight: 400;
}

.sort {
  color: #000000;
  font-family: "Open Sans";
  font-size: 14pt !important;
  font-weight: 400;
  font-size: 10pt;
}

.TableBkg {
  background-color: #fff;
  min-height: 80vh;
}

.nav-link {
  font-family: "Source Sans Pro", sans-serif;
  color: #9296ad;
  background-color: #fff;
  font-size: 10pt;
}

.nav-link.active {
  background-color: #055452;
  color: #fff !important;
  border-radius: 8px;
  font-weight: 600;
}

.nav-tabs {
  border-bottom: 0;
}
</style>