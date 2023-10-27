<script>
export default {
    name: 'WebhookForm',

    data() {
        return {
            formData: {
                nom: '',
                prenom: '',
                email: ''
            }
        };
    },

    methods: {
        async sendToTypedWebhook() {
            const webhookUrl = 'https://typedwebhook.tools/webhook/a6503797-4f06-4ccc-9147-5d1aa8a34f0b';

            try {
                const response = await fetch(webhookUrl, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json; charset=UTF-8'
                    },
                    body: JSON.stringify(this.formData)
                });

                if (response.ok) {
                    console.log('Données envoyées avec succès');
                    this.formData = { nom: '', prenom: '', email: '' }; // Réinitialiser le formulaire
                } else {
                    console.error('Erreur lors de l\'envoi des données', response);
                }
            } catch (error) {
                console.error('Erreur lors de l\'envoi des données', error);
            }
        }
    }
}
</script>

<template>
    <section>
        <div class="container">
            <div class="content">
                <div class="forms_group">
                    <form @submit.prevent="SendFormData">
                        <h2>Veuillez renseigner vos informations</h2>
                        <div class="input_group">
                            <h3>Nom</h3>
                            <input type="text" v-model="formData.nom">
                        </div>
                        <div class="input_group">
                            <h3>Prénom</h3>
                            <input type="text" v-model="formData.prenom">
                        </div>
                        <div class="input_group">
                            <h3>E-mail</h3>
                            <input type="email" v-model="formData.email">
                        </div>
                        <button class="button" @click="sendToTypedWebhook">TEST CONNEXION</button>
                    </form>
                </div> 
            </div>
        </div>
    </section>
</template>

<style scoped>
form{
    display: flex;
    flex-direction: column;
    align-items: center;
}
.container{
    display: flex;
    flex-direction: column;
    padding: 25px;
    margin-top: 100px;
    justify-content: center;
    align-items: center;
}
.content{
    width: 100%;
    max-width: 1024px;
    display: flex;
    flex-direction: row;
    justify-content: center;
}
.forms_group{
    width: 50%;
    min-width: 350px;
    border-radius: 25px;
    border-style: solid;
    border-color: aqua;
    padding: 25px;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.input_group{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 60%;
}
</style>