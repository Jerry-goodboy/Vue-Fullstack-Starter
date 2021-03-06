<template>
  <v-app>

    <v-navigation-drawer :clipped="$vuetify.breakpoint.mdAndUp" v-model="$app.drawer" fixed app>
      <v-list dense>
        <template v-for="item in $app.navigation">

          <v-subheader v-if="item.subheader" :key="item.subheader">{{ item.subheader }}</v-subheader>

          <!-- if children -->
          <v-list-group v-if="item.children" :key="item.text" :prepend-icon="item.icon" :disabled="item.disabled">
            <v-list-tile slot="activator">
              <v-list-tile-content>
                <v-list-tile-title>{{ item.text }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>

            <template v-for="child in item.children">

              <!-- if sub-children -->
              <v-list-group v-if="child.children" :key="child.text" :prepend-icon="child.icon" :disabled="child.disabled" sub-group>
                <v-list-tile slot="activator">
                  <v-list-tile-content>
                    <v-list-tile-title>{{ child.text }}</v-list-tile-title>
                  </v-list-tile-content>
                </v-list-tile>

                <v-list-tile v-for="subchild in child.children" :key="subchild.text" :to="subchild.route" :disabled="subchild.disabled">
                  <v-list-tile-action>
                    <v-icon>{{ subchild.icon }}</v-icon>
                  </v-list-tile-action>
                  <v-list-tile-content>
                    <v-list-tile-title>{{ subchild.text }}</v-list-tile-title>
                  </v-list-tile-content>
                </v-list-tile>
              </v-list-group>

              <!-- else not sub-children -->
              <v-list-tile v-else :key="child.text" :to="child.route" :disabled="child.disabled">
                <v-list-tile-action>
                  <v-icon>{{ child.icon }}</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                  <v-list-tile-title>{{ child.text }}</v-list-tile-title>
                </v-list-tile-content>
              </v-list-tile>

            </template>
          </v-list-group>

          <!-- else not children -->
          <v-list-tile v-else :key="item.text" :to="item.route" :disabled="item.disabled">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ item.text }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

        </template>
      </v-list>
    </v-navigation-drawer>

    <v-toolbar :clipped-left="$vuetify.breakpoint.mdAndUp" color="blue darken-3" dark app fixed>
      <v-toolbar-title class="ml-0 pl-3 vfs-toolbar-title">
        <v-toolbar-side-icon @click.stop="$app.drawer = !$app.drawer"></v-toolbar-side-icon>
        <router-link class="hidden-sm-and-down white--text vfs-router-link" to="/">Vue by Example</router-link>
      </v-toolbar-title>

      <v-text-field flat solo-inverted prepend-icon="search" label="Search" class="hidden-sm-and-down"></v-text-field>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>apps</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>notifications</v-icon>
      </v-btn>
      <v-btn icon href="https://github.com/Shyam-Chen/Vue-Fullstack-Starter" class="mr-3">
        <v-icon>fa fa-github</v-icon>
      </v-btn>
    </v-toolbar>

    <v-content>
      <v-container fluid class="vfs-container">
        <router-view></router-view>
      </v-container>
    </v-content>

    <v-footer inset class="pa-3 blue darken-3 white--text">
      <v-spacer></v-spacer>
      <div>Copyright &copy; {{ new Date().getFullYear() }} Vue by Example</div>
    </v-footer>

  </v-app>
</template>

<script>
// @flow

import { IApp } from './constants';

export default {
  computed: {
    $app(): IApp {
      return this.$store.state;
    },
  },
};
</script>

<style scoped>
.vfs-toolbar-title {
  width: 300px;
}

.vfs-router-link {
  text-decoration: none;
}

.vfs-container {
  height: 100%;
}
</style>
