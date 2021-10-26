<template>
    <jet-form-section @submitted="createTeam">
        <template #title>
            Informações para o baba
        </template>

        <template #description>
            Monte o seu baba.
        </template>

        <template #form>
            <div class="col-span-6">
                <jet-label value="Dono da bola" />

                <div class="flex items-center mt-2">
                    <img class="object-cover w-12 h-12 rounded-full" :src="$page.props.user.profile_photo_url" :alt="$page.props.user.name">

                    <div class="ml-4 leading-tight">
                        <div>{{ $page.props.user.name }}</div>
                        <div class="text-sm text-gray-700">{{ $page.props.user.email }}</div>
                    </div>
                </div>
            </div>

            <div class="col-span-6 sm:col-span-4">
                <jet-label for="name" value="Baba" />
                <jet-input id="name" type="text" class="block w-full mt-1" v-model="form.name" autofocus />
                <jet-input-error :message="form.errors.name" class="mt-2" />
            </div>

            <div class="col-span-6 sm:col-span-4">
                <jet-label for="local" value="Local" />
                <jet-input id="local" type="text" class="block w-full mt-1" v-model="form.locale" />
                <jet-input-error :message="form.errors.locale" class="mt-2" />
            </div>

            <div class="col-span-6 sm:col-span-4">
                <jet-label for="data_b" value="Data" />
                <jet-input id="data_b" type="date" class="block w-full mt-1" v-model="form.date_b" />
                <jet-input-error :message="form.errors.date_b" class="mt-2" />
            </div>

            <div class="col-span-6 sm:col-span-4">
                <jet-label for="hour" value="Horario" />
                <jet-input id="hour" type="time" class="block w-full mt-1" v-model="form.hour"/>
                <jet-input-error :message="form.errors.hour" class="mt-2" />
            </div>
        </template>

        <template #actions>
            <jet-button :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                Criar
            </jet-button>
        </template>
    </jet-form-section>
</template>

<script>
    import { defineComponent } from 'vue'
    import JetButton from '@/Jetstream/Button.vue'
    import JetFormSection from '@/Jetstream/FormSection.vue'
    import JetInput from '@/Jetstream/Input.vue'
    import JetInputError from '@/Jetstream/InputError.vue'
    import JetLabel from '@/Jetstream/Label.vue'

    export default defineComponent({
        components: {
            JetButton,
            JetFormSection,
            JetInput,
            JetInputError,
            JetLabel,
        },

        data() {
            return {
                form: this.$inertia.form({
                    name: '',
                    locale: '',
                    date_b: '',
                    hour: '',
                })
            }
        },

        methods: {
            createTeam() {
                this.form.post(route('teams.store'), {
                    errorBag: 'createTeam',
                    preserveScroll: true
                });
            },
        },
    })
</script>
