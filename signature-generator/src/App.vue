<script>
export default {
    data: function() {
        return {
                firstName: "",
                lastName: "",
                jobTitle: "",
                linksType: 0,
                customLink: "",
                photoLink: "",
                phoneNumber: "",
                address: 0,
                mail: ""
            };
    },
    computed: {
        firstNameGen: function () {
            return this.firstName || "Quentin";
        },
        lastNameGen: function () {
            return this.lastName || "Robert";
        },
        jobTitleGen: function () {
            return this.jobTitle || "Chargé de mission";
        },
    },
    methods:{
        preventBadCopy: function (event)
        {
            alert("Please, use the \"Copy signature into clipboard\" big blue button 🙂 !\n\n (If you use the context menu, your signature might be badly injured 💀)");
        },
        copySignature: function () {
            this.copyToClip(document.getElementById("render").innerHTML);
            alert("Your signature was copied into your clipboard. You can now Ctrl+V it on Gmail 😉\n\n(Or use \"right click/paste\" for the craziest ones out there 😬...)");
        },
        copyToClip: function (str) {
            function listener(e) {
                e.clipboardData.setData("text/html", str);
                e.clipboardData.setData("text/plain", str);
                e.preventDefault();
            }
            document.addEventListener("copy", listener);
            document.execCommand("copy");
            document.removeEventListener("copy", listener);
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="element form">
            <div class="form-field">
                <label for="firstName" class="field-name"> Prénom :</label>
                <input id="firstName" type="text" placeholder="Quentin" v-model="firstName">
            </div>
            <div class="form-field">
                <label for="lastName" class="field-name">Nom :</label>
                <input id="lastName" type="text" placeholder="Robert" v-model="lastName">
            </div>
            <div class="form-field">
                <label for="jobTitle" class="field-name">Poste :</label>
                <input id="jobTitle" type="text" placeholder="Head of Brand" v-model="jobTitle">
            </div>
            <div class="form-field">
                <label for="mail" class="field-name">Mail :</label>
                <input id="mail" type="text" placeholder="quentin.robert@gmail.com (optional)" v-model="mail">
            </div>
            <div class="form-field">
                <label for="phoneNumber" class="field-name">Téléphone :</label>
                <input id="phoneNumber" type="text" placeholder="+33 7 78 39 15 82 (optional)" v-model="phoneNumber">
            </div>
            <button class="button" @click="copySignature">
                Copy signature into clipboard
            </button>
        </div>
    </div>

    <div id="render" class="element" style=" height: fit-content" @select="preventBadCopy">
        <table style="border-collapse: collapse; border-spacing: 0; font-family: 'Helvetica', 'Arial', sans-serif; font-size:14px; line-height: 22px;">
            <tr>
                <td>
                    <div id="background">
                        <table style="border-collapse: collapse;border-spacing: 0;height: 60px;">
                            <tr>
                                <td>
                                    <div style="height: 10px"></div>
                                </td>
                                <td>
                                </td>
                            </tr>
                            <tr>
                                <td>
                                    <img class="logo" src ="./assets/logo.jpg" alt="Logo ABD"/>
                                </td>
                                <td style="vertical-align: top;padding: 0px 20px 20px;width: max-content" >
                                    <div style="color:#000000;">
                                        <span style="font-weight: bold; font-size: larger; color:#A6192E;">{{ firstNameGen }} {{ lastNameGen }}</span><br>
                                        <span style="color:#18191D;">{{ jobTitleGen }}</span><br>
                                        <span v-if="phoneNumber">
                                            <span style="color:#18191D;">{{phoneNumber}}</span><br>
                                        </span>
                                        <span v-if="mail">
                                            <span style="color:#18191D;">{{mail}}</span><br>
                                        </span>
                                        <a href="https://ecologie2024.eu" style="color:#18191D;font-weight: normal;">www.ecologie2024.eu</a>
                                    </div>
                                </td>
                            </tr>
                        </table>
                    </div>
                </td>
            </tr>
        </table>
    </div>

</template>

<style scoped>
html, body
{
    margin: 0;
    padding: 0;

    font-family:'Open Sans',Arial,sans-serif;
}

#header
{
    background: #ffffff;
    border-bottom: 1px solid #e0e0e0;
    height: 54px;
    margin-bottom: 25px;
}

.logo{
    height: 100px;
    width: 100px;
}

.container
{
    max-width: 980px;
    padding: 0 10px;
    margin: auto;
    display: flex;
    flex-direction: column;
}

.element
{
    border-radius: 4px;
    border: 1px solid #e0e0e0;
    background: #ffffff;
    padding: 20px;
}

.form h1
{
    font-size: 21px;
    font-weight: 100;
    color: #333333;
}

.form p
{
    font-size: 12px;
    margin: 4px 0;
}

a {
    color: #00A0FF;
    font-weight: bold;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

.form ol
{
    font-size: 12px;
    margin: 4px 0;
}

.form-wrapper
{
    display: flex;
    flex-wrap: wrap;
}

.form-field
{
    margin-right: 20px;
}

.field-name
{
    display: inline-block;
    width: 250px;
    font-size: 13px;
    font-weight: 600;
}

input, select
{
    padding: 9px;
    border: 1px solid #eeeeee;
    border-radius: 4px;
    margin: 2px 0;
    box-sizing: border-box;
}

input:not([type=checkbox]) {
    width: 340px;
}

input:focus, select:focus
{
    border: 1px solid #9e9e9e;
}

button.wide
{
    width: 400px;
}

button.with-margin
{
    margin: 8px auto !important;
}

button, .disabled
{
    cursor: not-allowed;
}

button
{
    height: 40px;
    border-radius: 4px;
    font-size: 12px;
    text-align: center;
    transition: all .2s ease-in-out;
    color: #194883;
    border: 1px solid #194883;
    background: #ffffff;
    text-transform: uppercase;
    width: 250px;
    cursor: pointer;
}

button:hover:not(.disabled)
{
    background: #194883;
    color: #ffffff;
}

.form
{
    position: relative;
}

.button
{
    margin: 16px auto auto;
    display: block;
}
</style>
