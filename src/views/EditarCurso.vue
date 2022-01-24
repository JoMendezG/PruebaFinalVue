<template>
  <div>
    <v-card>
      <v-card-title>
        <h1 class="display-1 mb-5 mt-5 mx-auto">
          Editar Curso {{ cursoSeleccionadoESP.data.Curso }}
        </h1>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-form ref="editForm" @submit.prevent="actualizarFormulario">
            <v-row>
              <v-col cols="12" md="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Codigo"
                  label="Código"
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="12">
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
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Costo"
                  type="number"
                  label="Costo"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Cupos"
                  type="number"
                  label="Cupos"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Inscritos"
                  type="number"
                  label="Inscritos"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-menu max-width="290">
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      :value="cursoSeleccionadoESP.data.Fecha"
                      label="Fecha"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="cursoSeleccionadoESP.data.Fecha"
                  ></v-date-picker>
                </v-menu>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Duracion"
                  label="Duración"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="cursoSeleccionadoESP.data.Foto"
                  label="URL Foto principal"
                  hint="Pega la URL de la Foton"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-switch
                  v-model="cursoSeleccionadoESP.data.Terminado"
                  label="Terminado"
                ></v-switch>
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
    actualizarCurso() {
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

      this.$store.commit("actualizarCurso", cursos);
      alert("Opinion actualizada");
    },
    actualizarFormulario() {
      actualizarData(this.id, this.cursoSeleccionadoESP.cursos);
      this.$router.push("/Admin");
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

<style>
div.v-card__text {
  background-color: white;
}
</style>
