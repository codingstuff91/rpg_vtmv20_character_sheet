<template>
    <b-tab-item label="Caractéristiques">
        <template #header>
            <img src="/img/level.png" class="mr-2" alt="">
            <span>Caractéristiques</span>
        </template>
        <!-- Affichage des attributs -->
        <h1 class="has-text-centered is-size-3 section_header">Attributs</h1>
        <div class="columns is-mobile">
            <div class="column is-4">
                <h2 class="has-text-centered is-size-5 category_header">Physiques</h2>
                <div :class="style" v-for="attribut in attributs_physiques" :key="attribut.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        rounded
                        @click="getDescription(attribut.id)"> 
                        {{ attribut.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled
                        v-model="attribut.niveau">
                    </b-rate>
                </div>
            </div>
            <div class="column is-4">
                <h2 class="has-text-centered is-size-5 category_header">Sociaux</h2>
                <div :class="style" v-for="attribut in attributs_sociaux" :key="attribut.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        rounded
                        @click="getDescription(attribut.id)"> 
                        {{ attribut.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled
                        v-model="attribut.niveau">
                    </b-rate>
                </div>
            </div>
            <div class="column is-4">
                <h2 class="has-text-centered is-size-5 category_header">Mentaux</h2>
                <div :class="style" v-for="attribut in attributs_mentaux" :key="attribut.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
                        rounded
                        @click="getDescription(attribut.id)"> 
                        {{ attribut.nom }}
                    </b-button>
                    <b-rate 
                        icon-pack="fas" 
                        :icon="icon"
                        spaced
                        :size="size"
                        disabled        
                        v-model="attribut.niveau">
                    </b-rate>
                </div>
            </div>
        </div>

        <h2 class="has-text-centered is-size-3 section_header">Capacités</h2>
        <div class="columns is-mobile">
            <div class="column is-4">
                <h2 class="has-text-centered is-size-5 category_header">Physiques</h2>
                <div :class="style" v-for="capacite in capacites_talents" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
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
                <h2 class="has-text-centered mb-2 is-size-5 category_header">Sociales</h2>
                <div :class="style" v-for="capacite in capacites_competences" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
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
                <h2 class="has-text-centered mb-2 is-size-5 category_header">Mentales</h2>
                <div :class="style" v-for="capacite in capacites_connaissances" :key="capacite.id">
                    <b-button 
                        icon-left="question-circle" 
                        size="is-small"
                        type="is-danger"
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
                attributs_physiques : [],
                attributs_sociaux : [],
                attributs_mentaux: [],
                capacites_talents : [],
                capacites_competences : [],
                capacites_connaissances : [],
                icon : 'tint',
                size : 'is-medium',
                style : 'my-4 is-flex is-flex-direction-column is-justify-content-center is-align-items-center'
            }
        },
        props: {
            personnage: {
                type: Object,
            },
        },
        mixins: [CaracteristiquesMixin],

        methods: {
            getDescription(attribut_id) {
                this.$emit('get_description',attribut_id)
            }
        },
        async mounted(){
            await this.getCaracteristiquesLevels(this.personnage.id, 'Attributs_physiques', 'attributs_physiques')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Attributs_mentaux', 'attributs_mentaux')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Attributs_sociaux', 'attributs_sociaux')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_talents', 'capacites_talents')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_compétences', 'capacites_competences')
            await this.getCaracteristiquesLevels(this.personnage.id, 'Capacités_connaissances', 'capacites_connaissances')
        }
    }
</script>
<style lang="scss" scoped>
    $rate-color : "red";
    $rate-color-active : "green";

.section_header{
    font-family: 'Vampiro One', cursive;
    color:#f14668;
}

.category_header{
    font-family: 'Vampiro One', cursive;
}
</style>