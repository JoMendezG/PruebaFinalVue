<template>
  <div>
    <v-card>
      <v-card-title>
        <span class="text-h5"
          >Editar Curso {{ cursoSeleccionadoESP.data.Curso }}</span
        >
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-form ref="editForm" @submit.prevent="editCourse">
            <v-row>
              <v-col cols="12" md="3">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Codigo"
                  label="Código"
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="9">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Curso"
                  label="Nombre"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Descripcion"
                  label="Descripción"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Costo"
                  type="number"
                  min="0"
                  max="1000000"
                  step="10000"
                  label="Costo"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Cupos"
                  type="number"
                  min="0"
                  label="Cupos"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Inscritos"
                  type="number"
                  min="0"
                  label="Inscritos"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-menu max-width="290">
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      :value="cursoSeleccionadoESP.data.Fecha"
                      label="Fecha"
                      prepend-icon="mdi-calendar-range"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="cursoSeleccionadoESP.data.Fecha"
                  ></v-date-picker>
                </v-menu>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Duracion"
                  label="Duración"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-switch
                  v-model="cursoSeleccionadoESP.data.Terminado"
                  label="Terminado"
                ></v-switch>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Foto"
                  label="URL Foto principal"
                  hint="Pega la URL de la Foton"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-card-actions class="mt-5 d-flex flex-row-reverse">
              <div class="d-flex flex-row">
                <v-btn
                  color="blue darken-1"
                  text
                  @click="$router.push(`/admin`)"
                >
                  Cancelar
                </v-btn>
                <v-btn color="primary" type="submit"> Editar Curso </v-btn>
              </div>
            </v-card-actions>
          </v-form>
        </v-container>
        <p class="text-end mr-5">*Todos los campos son requeridos</p>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import { actualizarData } from "../firebase/firestore";
export default {
  props: ["id"],
  data() {
    return {
      cursos: {
        Codigo: "",
        Curso: "",
        Descripcion: "",
        Costo: "",
        Cupos: "",
        Inscritos: "",
        Fecha: "",
        Duracion: "",
        Terminado: "",
        Foto: "",
      },
    };
  },
  methods: {
    upadateCourse() {
      let cursos = {
        index: this.id,
        course: {
          Codigo: this.Codigo,
          Curso: this.Codigo,
          Descripcion: this.Descripcion,
          Costo: this.Costo,
          Cupos: this.Cupos,
          Inscritos: this.Inscritos,
          Fecha: this.Fecha,
          Duracion: this.Duracion,
          Terminado: this.Terminado,
          Foto: this.Foto,
        },
      };

      this.$store.commit("upadateCourse", cursos);
      alert("Opinion actualizada");
    },
    editCourse() {
      // this.upadateCourse();
      actualizarData(this.id, this.cursoSeleccionadoESP.cursos);
      this.$router.push("/admin");
    },
  },
  created() {},
  computed: {
    traerId() {
      return this.$route.params.id;
    },
    cursoSeleccionadoESP() {
      return this.$store.getters.filtrarCurso(this.traerId);
    },
  },
  mounted() {
    this.cursoSeleccionadoESP;
  },
};
</script>
