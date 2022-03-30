<template>
  <div class="settings">
    <h1>Google Functions</h1>
    <button v-on:click="getAuthToken()">Get Auth Token</button>
     <button v-on:click="getProfile()">Get User Profile</button>
    <button v-on:click="getBasicData()">Get Basic Data</button>
     <button v-on:click="getContacts()">Get User's Contacts</button>
     <button v-on:click="readNotes()">Read Speaker Notes</button>
     <button v-on:click="insertPlaceholder()">Insert Placeholder</button>
    <!--<button v-on:click="sendFakeData()">Send some data to Proxy</button>-->
  </div>
</template>
<script>
import { mapState } from 'vuex'
import listenForUser from "../include/userInteractionListeners.js";
export default {
    data:function(){
        return {
            API_KEY:"AIzaSyDzX5Wuct1_Hh9TunabzaVSc52zLLwCyZE",
            user_signed_in:false
        }
    },
    computed: mapState({
		did: (state) => state.user.did,
	}),
    methods: {
        getAuthToken: function(){
            chrome.identity.getAuthToken({ interactive: true }, function (token) {
                console.log(token);
            });
        },
        getProfile: function(){
            chrome.identity.getProfileUserInfo({ accountStatus: 'ANY' }, function (user_info) {
            console.log(user_info);
            });
        },
        readNotes:async function(){
            let scopedThis=this
            let didToken = await listenForUser.getdidToken()
            console.log(didToken,'user!!')
            const msg = {
                action:"readNotes",
                attributes:{
                    presentationId:"13_Q1JUpuLAa90QeDWsiR_OWucSCRhZ29iCT28mJocGY",
                    userId:didToken
                },
                vars:{
                    GOOGLE_API_KEY:this.API_KEY,
                    GSLIDES_API_URL:"https://slides.googleapis.com/v1/presentations"
                }
            }
            chrome.runtime.sendMessage(msg, function(response){
                scopedThis.sendToDoppio(response)
                });
        },
        getBasicData:function(){
            const msg = {
                action:"getBasicData",
                attributes:{
                    presentationId:"13_Q1JUpuLAa90QeDWsiR_OWucSCRhZ29iCT28mJocGY"
                },
                vars:{
                    GOOGLE_API_KEY:this.API_KEY,
                    GSLIDES_API_URL:"https://slides.googleapis.com/v1/presentations"
                }
            }
            chrome.runtime.sendMessage(msg,resp=>console.log(resp));
        },
        insertPlaceholder:function(){
            const msg = {
                action:"insertPlaceholder",
                attributes:{
                    presentationId:"13_Q1JUpuLAa90QeDWsiR_OWucSCRhZ29iCT28mJocGY",
                    slideId:"p",
                    objectId:"abcdefg",
                    mediaURL:"https://media.istockphoto.com/photos/letter-a-picture-id1296374556?s=612x612"
                },
                vars:{
                    GOOGLE_API_KEY:this.API_KEY,
                    GSLIDES_API_URL:"https://slides.googleapis.com/v1/presentations"
                }
            }
            chrome.runtime.sendMessage(msg, function (response){console.log(response)});
        },
        sendToDoppio:function(presentationData){
            const msg = {
                action:"sendToDoppio",
                attributes:{
                    presentationData:presentationData
                },       
            }     
            chrome.runtime.sendMessage(msg,resp=>console.log(resp));
        }
    }
}
</script>