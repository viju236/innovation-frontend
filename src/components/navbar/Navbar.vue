<template>
  <div>
    <nav id="navBar">
      <ul>
        <li><va-button :to="{name: 'home_page'}">
          Home Page
        </va-button></li>
        <li><va-button :to="{name: 'view_report'}">
          View Report
        </va-button></li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  
};
</script>

<style lang="scss" scoped>
#navBar {
  background-color: lightskyblue;
}

#navBar ul {
  overflow: auto;
  border: solid 2px gray;
  border-radius: 4px;
}

#navBar li {
  float: left;
  list-style: none;
  padding: 15px;
}

#navBar li a {
  text-decoration: none;
  color: black;
}


#navBar #searchBox {
  float: right;
  margin: 13px 50px;
}

#navBar #search {
  border: solid 2px gray;
  border-radius: 4px;
  padding: 2px 4px;
  width: 200px;
}

#navBar label {
  margin: 2px;
}
</style>