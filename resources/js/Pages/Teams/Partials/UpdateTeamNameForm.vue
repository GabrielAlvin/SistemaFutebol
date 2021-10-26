<template>
    <jet-form-section @submitted="updateTeamName">
        <template #title>
            Informações
        </template>

        <template #description>
            Crie seu baba.
        </template>

        <template #form>
            <!-- Team Owner Information -->
            <div class="col-span-6">
                <jet-label value="Dono da bola" />

                <div class="flex items-center mt-2">
                    <img class="w-12 h-12 rounded-full object-cover" :src="team.owner.profile_photo_url" :alt="team.owner.name">

                    <div class="ml-4 leading-tight">
                        <div>{{ team.owner.name }}</div>
                        <div class="text-gray-700 text-sm">{{ team.owner.email }}</div>
                    </div>
                </div>
            </div>

            <!-- Team Name -->
            <div class="col-span-6 sm:col-span-4">
                <jet-label for="name" value="Nome do Baba" />

                <jet-input id="name"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.name"
                            :disabled="! permissions.canUpdateTeam" />

                <jet-input-error :message="form.errors.name" class="mt-2" />
            </div>

            <!-- local Name -->
            <div class="col-span-6 sm:col-span-4">
                <jet-label for="locale" value="Local" />

                <jet-input id="locale"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.locale"
                            :disabled="! permissions.canUpdateTeam" />

                <jet-input-error :message="form.errors.locale" class="mt-2" />
            </div>


            <!-- data -->
            <div class="col-span-6 sm:col-span-4">
                <jet-label for="date_b" value="Data" />

                <jet-input id="date_b"
                            type="date"
                            class="mt-1 block w-full"
                            v-model="form.date_b"
                            :disabled="! permissions.canUpdateTeam" />

                <jet-input-error :message="form.errors.date_b" class="mt-2" />
            </div>

            <!-- houras -->
            <div class="col-span-6 sm:col-span-4">
                <jet-label for="hour_b" value="Horario" />

                <jet-input id="hour_b"
                            type="time"
                            class="mt-1 block w-full"
                            v-model="form.hour_b"
                            :disabled="! permissions.canUpdateTeam" />

                <jet-input-error :message="form.errors.hour_b" class="mt-2" />
            </div>
        </template>

        <template #actions v-if="permissions.canUpdateTeam">
            <jet-action-message :on="form.recentlySuccessful" class="mr-3">
                Salvo
            </jet-action-message>

            <jet-button :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                Salvar
            </jet-button>
        </template>
    </jet-form-section>
</template>

<script>
    import { defineComponent } from 'vue'
    import JetActionMessage from '@/Jetstream/ActionMessage'
    import JetButton from '@/Jetstream/Button'
    import JetFormSection from '@/Jetstream/FormSection'
    import JetInput from '@/Jetstream/Input'
    import JetInputError from '@/Jetstream/InputError'
    import JetLabel from '@/Jetstream/Label'

    export default defineComponent({
        components: {
            JetActionMessage,
            JetButton,
            JetFormSection,
            JetInput,
            JetInputError,
            JetLabel,
        },

        props: ['team', 'permissions'],

        data() {
            return {
                form: this.$inertia.form({
                    name: this.team.name,
                    locale: this.team.locale,
                    hour_b: this.team.hour_b,
                    date_b: this.team.date_b,
                })
            }
        },

        methods: {
            updateTeamName() {
                this.form.put(route('teams.update', this.team), {
                    errorBag: 'updateTeamName',
                    preserveScroll: true
                });
            },
        },
    })
</script>
