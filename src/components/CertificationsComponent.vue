<template>
    <div>
        <div class="card">
            <div class="card-body">
                <div class="d-flex justify-content-between mb-4">
                    <h3 class="font-weight-normal">Certifications</h3>

                    <span class="cursor-pointer" @click="toggleCreate" v-if="isLinkVisible">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit text-secondary btn-icon-prepend">
                            <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
                            <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
                        </svg> Ajouter une certification
                    </span>
                </div>

                <div v-if="isShow">
                    <div v-for="certification in certifications" :key="certification.id">
                        <certification-item :certification="certification" :key="certification.id"></certification-item>
                    </div>
                </div>

                <transition name="dropdown-fade">
                    <form @submit="AddRecord" v-if="isVisible">

                        <div class="form-label-group">
                            <input type="text" id="diplomaName" class="form-control" name="title" v-model="certification.title" placeholder="Certification suivie" required="required" autocomplete="off" autofocus>
                            <label for="diplomaName">Certification suivie</label>
                        </div>
                        <div class="form-label-group">
                            <input type="text" id="schoolProvider" name="provider" v-model="certification.provider" class="form-control" placeholder="Organisme de certification" required="required" autocomplete="off">
                            <label for="schoolProvider">Organisme de certification</label>
                        </div>
                        <div class="form-row align-items-center">
                            <div class="col-auto my-1">
                                <div class="form-label-group">
                                    <input type="date" id="dateEarned" :disabled="disabled == 1" v-model="certification.date_earned" class="form-control" placeholder="Date Earned" required="required" autocomplete="off">
                                    <label for="dateEarned">Date Earned</label>
                                </div>
                            </div>

                            <div class="col-auto my-1">
                                <div class="custom-control custom-checkbox mr-sm-2">
                                    <input type="checkbox" @click="disabled = (disabled + 1) % 2" v-model="certification.ongoing" class="custom-control-input" id="ongoing">
                                    <label class="custom-control-label" for="ongoing">Toujours en cours</label>
                                </div>
                            </div>
                        </div>
                        <div class="form-label-group mb-4">
                            <input type="text" id="CertificationLink" class="form-control" v-model="certification.certification_link" placeholder="Certification Link">
                            <label for="CertificationLink">Certification Link</label>
                        </div>

                        <button type="submit" class="btn btn-primary text-secondary">Valider</button>
                        <button type="button" @click="toggleCreate" class="btn btn-light text-secondary float-right">Annuler</button>
                    </form>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    import certification from './CertificationItem';
    export default {
        components: {
            'certification-item': certification,
        },
        data() {
            return {
                certifications: [
                    { title: 'Certified Web Professional', provider: 'International Webmasters Association', date_earned: '', ongoing: true, certification_link: '' },
                    { title: 'Javascript Development Certified Professional', provider: 'Learning Tree International', date_earned: 2020, ongoing: false, certification_link: '' },
                    { title: 'E-Commerce Developer (ECD)', provider: 'ETA International', date_earned: 2019, ongoing: false, certification_link: '' },
                ],
                certification: {
                    title: '',
                    provider: '',
                    date_earned: '',
                    ongoing: '',
                    certification_link: ''
                },
                isVisible: false,
                isShow: true,
                isActive: false,
                isLinkVisible: true,
                disabled: 0,
            }
        },
        methods: {
            toggleCreate () {
                if (!this.isActive) {
                    this.isVisible = !this.isVisible
                    this.isShow = !this.isShow
                    this.isLinkVisible = !this.isLinkVisible
                } else {
                    this.isVisible = this.isVisible
                    this.isShow = this.isShow
                    this.isLinkVisible = this.isLinkVisible
                }
            },
            AddRecord: function (e) {
                
                e.preventDefault()
            },
        }
    }
</script>

<style scoped>
    .btn {
        font-family: "Nunito", sans-serif;
        letter-spacing: 2px;
        text-transform: normal;
        color: white;
    }
    .btn-primary {
        color: #212529;
        background-color: #25fde9;
        border-color: #25fde9;
    }

    .dropdown-fade-enter-active, .dropdown-fade-leave-active {
        transition: all .1s ease-in-out;
    }
    .dropdown-fade-enter, .dropdown-fade-leave-to {
        opacity: 0;
        transform: translateY(-12px);
    }

    .cursor-pointer{
        cursor: pointer;
    }

</style>