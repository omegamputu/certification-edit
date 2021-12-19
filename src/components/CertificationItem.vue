<template>
    <div>
        <div class="media mb-2">
            <div class="bg-light p-3 rounded shadow-none mr-3">
                <i class="fas fa-award fa-2x text-secondary"></i>
            </div>
            <div class="media-body">
                <div class="d-flex flex-row">
                    <h5 class="mr-2">{{ certification.title }}</h5>
                    <svg @click="selectedItem" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit text-secondary cursor-pointer btn-icon-prepend">
                        <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
                        <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
                    </svg>
                </div>
                <h6 class="font-weight-normal text-secondary">{{  certification.provider }}</h6>
                <i class="far fa-calendar"></i>
                <small class="text-muted">
                    {{ certification.date_earned ? certification.date_earned : "Ongoing" }}
                </small>
            </div>
        </div>
        <transition name="dropdown-fade" v-if="isSelected">
            <form v-on:submit.prevent="UpdateRecord(certification)">
                <div class="form-label-group">
                    <input type="text" id="certName" class="form-control" v-model="certification.title" placeholder="Certification suivie" autofocus>
                    <label for="certName">Certification suivie</label>
                </div>
                <div class="form-label-group">
                    <input type="text" id="updateSchoolProvider" v-model="certification.provider" class="form-control" placeholder="Organisation de certification">
                    <label for="updateSchoolProvider">Organisation de certification</label>
                </div>
                <div class="form-row align-items-center">
                    <div class="col-auto my-1">
                        <div class="form-label-group">
                            <input type="date" id="updateDateEarned" :disabled="disabled == 1" v-model="certification.date_earned" class="form-control" placeholder="Date Earned">
                            <label for="updateDateEarned">Date Earned</label>
                        </div>
                    </div>
                    <div class="col-auto my-1">
                        <div class="custom-control custom-checkbox mr-sm-2">
                            <input type="checkbox" @click="disabled = (disabled + 1) % 2" v-model="certification.ongoing" class="custom-control-input" id="updateOngoing">
                            <label class="custom-control-label text-secondary" for="updateOngoing">Toujours en cours</label>
                        </div>
                    </div>
                </div>
                <div class="form-label-group mb-4">
                    <input type="text" id="UpdateCertLink" class="form-control" v-model="certification.certification_link" placeholder="Certification Link">
                    <label for="UpdateCertLink">Certification Link</label>
                </div>

                <div class="form-group">
                    <button type="submit" class="btn btn-primary">Save changes</button>
                    <button type="button" class="btn btn-light text-secondary" @click="selectedItem">Cancel</button>
                    <button type="button" class="btn btn-danger float-right" @click="DeleteRecord(certification)">Delete</button>
                </div>
            </form>
        </transition>
    </div>
</template>

<script>
    export default {
        props: ['certification'],
        data () {
            return {
                disabled: 0,
                isSelected: false,
                isActive: false,
            }
        },
        methods: {
            selectedItem: function () {
                if (!this.isActive) {
                    this.isSelected = !this.isSelected
                } else {
                    this.isSelected = this.isSelected
                }
            },
            UpdateRecord:  function(certification) {
                
            },
            DeleteRecord: function (certification) {
                
            }
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

    .cursor-pointer{
        cursor: pointer;
    }

    .dropdown-fade-enter-active, .dropdown-fade-leave-active {
        transition: all .1s ease-in-out;
    }
    .dropdown-fade-enter, .dropdown-fade-leave-to {
        opacity: 0;
        transform: translateY(-12px);
    }
</style>