<template>
    <b-tab-item label="Capacités">
        <!-- Affichage des compétences -->
        <h1 class="has-text-centered is-size-4">Capacités</h1>
        <div class="columns is-mobile">
            <div class="column is-4">
                <h2 class="has-text-centered is-size-5 mt-4">Physiques</h2>
                <div :class="box_style" v-for="capacite in capacites_talents" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        class="mt-2"
                        rounded
                        @click="getDescription(capacite.id)"> 
                        {{ capacite.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled
                        v-model="capacite.niveau">
                    </b-rate>
                </div>
            </div>
            <div class="column is-4">
                <h2 class="has-text-centered mb-4 is-size-5 mt-4">Sociales</h2>
                <div :class="box_style" v-for="capacite in capacites_competences" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        class="mt-2"
                        rounded
                        @click="getDescription(capacite.id)"> 
                        {{ capacite.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled
                        v-model="capacite.niveau">
                    </b-rate>
                </div>
            </div>
            <div class="column is-4">
                <h2 class="has-text-centered mb-4 is-size-5 mt-4">Mentales</h2>
                <div :class="box_style" v-for="capacite in capacites_connaissances" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        class="mt-2"
                        rounded
                        @click="getDescription(capacite.id)"> 
                        {{ capacite.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled
                        v-model="capacite.niveau">
                    </b-rate>
                </div>
            </div>
        </div>
    </b-tab-item>
</template>

<script>
import CaracteristiquesMixin from '../mixins/caracteristiquesMixin.vue'

    export default {
        data() {
            return {
                capacites_talents : [],
                capacites_competences : [],
                capacites_connaissances : [],
                size : 'is-medium',
                icon : 'tint',
                box_style : 'my-4 is-flex is-flex-direction-column is-justify-content-center is-align-items-center'
            }
        },
        props: {
            personnage: {
                type: Object,
            },
        },
        methods: {
            getDescription(capacite_id) {
                this.$emit('get_description',capacite_id)
            }
        },
        mixins: [CaracteristiquesMixin],
        async mounted(){
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_talents', 'capacites_talents')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_compétences', 'capacites_competences')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_connaissances', 'capacites_connaissances')
        }
    }
</script>