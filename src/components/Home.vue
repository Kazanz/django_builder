<template>

  <v-container fluid class="px-0 mx-0">

    <v-layout row align-center justify-center fill-height class="text-xs-center">
      <v-flex xs12 >
        <div class="display-4 hidden-sm-and-down" ><django-builder-title /></div>
        <div class="display-2 hidden-md-and-up" ><django-builder-title /></div>
     </v-flex>
    </v-layout>

    <v-layout align-space-around justify-center row fill-height wrap
      v-if="this.$store.getters.loaded()">
      <v-flex xs12 md6 lg3 v-for="(project, i) in this.$store.getters.projectsData()"
        :key="project.id" elevation="6"
        class="ma-2" >

        <v-card :to="{ name: 'Project', params: { id: project.id } }" min-height="250px">
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">{{project.name}}</h3>
              <div>{{project.description}}&nbsp;</div>
            </div>
          </v-card-title>

          <v-img :src="images[i % images.length]" aspect-ratio="2.75" height="180"></v-img>

          <!--template v-for="(d, app) in project.apps">
            <v-card-text v-for="(dd, model) in $store.getters.appData(app).models">
              <v-icon style="font-size:1.0em">fas fa-database</v-icon>
              {{$store.getters.appData(app).name}}.{{$store.getters.modelData(model).name}}
            </v-card-text>
          </template-->

        </v-card>
      </v-flex>

      <v-flex xs12 md12 lg12 v-if="this.$store.getters.projectsData().length > 0"
        elevation="6" class="ma-3 text-xs-center">
        <v-btn color="primary" @click="showAddProjectDialog" class="mb-4">
          <v-icon>add</v-icon> Create a New Project
        </v-btn>
      </v-flex>

      <v-flex xs12 md6 lg3 v-if="this.$store.getters.projectsData().length === 0"
        class="text-xs-center ma-2 font-weight-medium">
        <v-card >
          <v-card-title primary-title>
            Welcome to Django Builder, you dont seem to have any projects. To start just...
          </v-card-title>
          <v-card-text class="text-xs-center">
            <v-btn color="primary" @click="showAddProjectDialog" class="mb-4">
              <v-icon>add</v-icon> Create a New Project
            </v-btn>
          </v-card-text>
          <v-img :src="images[0]" aspect-ratio="2.75" height="180"></v-img>
        </v-card>
      </v-flex>

    </v-layout>
  </v-container>
</template>
<script>

import addProjectMixin from '@/mixins/AddProject'

export default {
  mixins: [addProjectMixin],
  data () {
    return {
      images: [
        'placeimg_1000_600_grayscale_tech.png',
        'placeimg_1000_600_grayscale_arch.png',
        'placeimg_1000_600_grayscale_arch2.png',
      ],
    }
  }
}
</script>
