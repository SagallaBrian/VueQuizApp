<template>
  <div class="pt-5 pb-3">
    <b-container fluid="lg">
      <b-navbar toggleable="lg">
         <b-navbar-brand href="#" class="text-danger">Simple Quiz</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
            <b-nav-item href="#">About Page</b-nav-item>
            <!-- <b-nav-item href="#" disabled>Disabled</b-nav-item> -->
            </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template v-slot:button-content>
                <em>User</em>
              </template>
              <b-dropdown-item href="#">Profile</b-dropdown-item>
              <b-dropdown-item href="#">Sign Out</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Heada",
  props: {
    HeaderMesa: {
      type: String,
      default: "Header Message",
    },
  },
};
</script>