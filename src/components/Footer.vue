<template>
  <footer>
    <div class="container pt-5">
      <div class="row" style="display: flex; flex-direction: row; justify-content: space-between;">
        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold pb-2">Get to Know Us</li>
            <li><a class="footer-link font-weight-light" href="#">Fabian</a></li>
            <li><a class="footer-link font-weight-light" href="#">Tea</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-6">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Connect With Us</li>
            <li><a class="footer-link font-weight-light" href="#">Email</a></li>
            <li><a class="footer-link font-weight-light" href="#">Github</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">LinkedIn</a><br></li>
          </ul>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div class="text-center py-5">
            <img id="logo" src="../assets/icon.png" />
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name : "Footer"
}
</script>

<style>
footer {
  margin-top : 100px;
  background-color:#232F3E;
  font-size:16px;
}

li {
  padding-left: 0;
  padding-bottom: 10px;
}

a {
  text-decoration: none;
}

.footer-link {
  color: #DDD;
}

#logo {
  width: 300px;
}

footer {
  font-family: 'Roboto', sans-serif;
}


</style>
