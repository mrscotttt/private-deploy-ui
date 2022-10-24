<template>
    <div class="p-16 dragFont">
        <div class="rounded-lg dragArea w-full justify-center  p-8 text-black drop-shadow-2xl backdrop-blur-md bg-white/60">
            <!-- {{ticketGroup}} -->
            <div class="grid grid-cols-4 gap-2">
                  <div>
                    <div>
                      <h5 class="mb-8 text-center text-2xl font-bold tracking-tight text-gray-900">
                      <font-awesome-icon class="text-indigo-600" icon="fa-solid fa-flag" />{{' '}}Pending<emptyBox/>
                      </h5>
                    </div>
                    <div class="rounded-lg dragInnerArea justify-center p-4 text-black drop-shadow-2xl bg-white/60 overflow-y-auto overflow-x-auto">
                      <draggable :list="ticketGroup.pending" group="people" @change="log($event,'pending')">
                        <div
                          class="list-group-item"
                          v-for="(element, index) in ticketGroup.pending"
                          :key="element.name"
                        >
                          <div class="">
                            <a class="w-full flex mt-6 rounded-3xl inline-block overflow-hidden shadow-xl rounded-lg cursor-pointer transition ease-in-out hover:-translate-y-1 hover:scale-102 duration-300">
                                <div class="bg-indigo-600 w-3">
                                </div>
                                <div class="bg-white w-full">
                                    <div class="text-center px-3 pb-6 pt-2">
                                        <div class="mt-2 font-bold text-slate-700">
                                          {{element.title}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.description}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.createTimeFormat}}
                                        </div>
                                    </div>
                                    <div class="flex justify-center pb-3 text-slate-700">
                                        <div>
                                          <previewTicket :parentmessage="element"></previewTicket>
                                        </div>

                                        <div>
                                          <addTicket :parentmessage="element"></addTicket>
                                        </div>
                                    </div>
                                </div>
                            </a>
                        </div>
                        </div>
                      </draggable>
                    </div>
                  </div>
                  <div>
                    <div>
                      <h5 class="mb-8 text-center text-2xl font-bold tracking-tight text-gray-900">
                        <font-awesome-icon class="text-yellow-500" icon="fa-solid fa-circle-check" />{{' '}}Accepted
                      </h5>
                    </div>
                    <div class="rounded-lg dragInnerArea justify-center p-4 text-black drop-shadow-2xl bg-white/60 overflow-y-auto overflow-x-auto">
                      <draggable :list="ticketGroup.accepted" group="people" @change="log($event,'accepted')">
                        <div
                          class="list-group-item"
                          v-for="(element, index) in ticketGroup.accepted"
                          :key="element.name"
                        >
                          <div class="">
                            <a class="w-full flex mt-6 rounded-3xl inline-block overflow-hidden shadow-xl rounded-lg cursor-pointer transition ease-in-out hover:-translate-y-1 hover:scale-102 duration-300">
                                <div class="bg-yellow-500 w-3">
                                </div>
                                <div class="bg-white w-full">
                                    <div class="text-center px-3 pb-6 pt-2">
                                        <div class="mt-2 font-bold text-slate-700">
                                          {{element.title}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.description}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.createTimeFormat}}
                                        </div>
                                    </div>
                                    <div class="flex justify-center pb-3 text-slate-700">
                                        <div>
                                          <previewTicket :parentmessage="element"></previewTicket>
                                        </div>

                                        <div>
                                          <addTicket :parentmessage="element"></addTicket>
                                        </div>
                                    </div>
                                </div>
                            </a>
                        </div>
                        </div>
                      </draggable>

                    </div>
                  </div>
                  <div>
                    <div>
                      <h5 class="mb-8 text-center text-2xl font-bold tracking-tight text-gray-900">
                        <font-awesome-icon class="text-teal-600" icon="fa-solid fa-thumbs-up" />{{' '}}Resolved
                      </h5>
                    </div>
                    <div class="rounded-lg dragInnerArea justify-center p-4 text-black drop-shadow-2xl bg-white/60 overflow-y-auto overflow-x-auto">
                      <draggable :list="ticketGroup.resolved" group="people" @change="log($event,'resolved')">
                        <div
                          class="list-group-item"
                          v-for="(element, index) in ticketGroup.resolved"
                          :key="element.name"
                        >
                          <div class="">
                            <a class="w-full flex mt-6 rounded-3xl inline-block overflow-hidden shadow-xl rounded-lg cursor-pointer transition ease-in-out hover:-translate-y-1 hover:scale-102 duration-300">
                                <div class="bg-teal-600 w-3">
                                </div>
                                <div class="bg-white w-full">
                                    <div class="text-center px-3 pb-6 pt-2">
                                        <div class="mt-2 font-bold text-slate-700">
                                          {{element.title}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.description}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.createTimeFormat}}
                                        </div>
                                    </div>
                                    <div class="flex justify-center pb-3 text-slate-700">
                                        <div>
                                          <previewTicket :parentmessage="element"></previewTicket>
                                        </div>

                                        <div>
                                          <addTicket :parentmessage="element"></addTicket>
                                        </div>
                                    </div>
                                </div>
                            </a>
                        </div>
                        </div>
                      </draggable>
                    </div>
                  </div>
                  <div>
                    <div>
                      <h5 class="mb-8 text-center text-2xl font-bold tracking-tight text-gray-900">
                        <font-awesome-icon class="text-red-700" icon="fa-solid fa-circle-xmark" />{{' '}}Rejected
                      </h5>
                    </div>
                    <div class="rounded-lg dragInnerArea justify-center p-4 text-black drop-shadow-2xl bg-white/60 overflow-y-auto overflow-x-auto">
                      <draggable :list="ticketGroup.rejected" group="people" @change="log($event,'rejected')">
                        <div
                          class="list-group-item"
                          v-for="(element, index) in ticketGroup.rejected"
                          :key="element.name"
                        >
                          <div class="">
                            <a class="w-full flex mt-6 rounded-3xl inline-block overflow-hidden shadow-xl rounded-lg cursor-pointer transition ease-in-out hover:-translate-y-1 hover:scale-102 duration-300">
                                <div class="bg-red-700 w-3">
                                </div>
                                <div class="bg-white w-full">
                                    <div class="text-center px-3 pb-6 pt-2">
                                        <div class="mt-2 font-bold text-slate-700">
                                          {{element.title}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.description}}
                                        </div>
                                        <div class="mt-2 font-light text-slate-700">
                                          {{element.createTimeFormat}}
                                        </div>
                                    </div>
                                    <div class="flex justify-center pb-3 text-slate-700">
                                        <div>
                                          <previewTicket :parentmessage="element"></previewTicket>
                                        </div>

                                        <div>
                                          <addTicket :parentmessage="element"></addTicket>
                                        </div>
                                    </div>
                                </div>
                            </a>
                        </div>
                        </div>
                      </draggable>
                    </div>
                  </div>
          </div>
        </div>
    </div>
  </template>

  <script>
  import draggable from "vuedraggable";
  import axios from 'axios'
  import previewTicket from './previewTicket';
  import addTicket from './addTicket';
  import addNewTicket from './addNewTicket';
  import moment from 'moment';
  import emptyBox from '../assets/empty-box.svg';

  export default {
    name: 'dragTicket',
    components: {draggable,previewTicket,addTicket,addNewTicket,emptyBox},
    data: () => ({
      previewDialog: false,
      report: [],
      ticketCard: [],
      ticketGroup: {pending: [],accepted: [],resolved: [],rejected: []}
    }),
    created: async function(){
        await this.hookticket()
        await this.groupUp()
    },
    methods: {
        async log(evt,status) {
            if(evt.added){
              let updateParams = evt.added.element
              updateParams.status = status
              try{
                let tkt = await axios.post('/updateStatusTicket',updateParams)
                // console.log("update success")
                await this.hookticket()
                await this.groupUp()
              }
              catch(err){
                // console.log("update fail",err)
              }
            }
        },
        async hookticket() {
            try{
                let tkt = await axios.get('/ticket')
                this.ticketCard = tkt.data.Items
                if(this.ticketCard.length>0){this.ticketCard.sort((a, b) => a.createTime - b.createTime);}
            }
            catch(err){
                this.ticketCard = []
            }
        },
        async groupUp() {
            let t = await this.ticketCard
            let g = {pending: [],accepted: [],resolved: [],rejected: []}
            for(var i=0;i<t.length;i++){
                t[i].createTimeFormat = moment(t[i].createTime).format("DD MMM YYYY hh:mm")
                if(t[i].status=="pending"){(g.pending).push(t[i])}
                else if(t[i].status=="accepted"){(g.accepted).push(t[i])}
                else if(t[i].status=="resolved"){(g.resolved).push(t[i])}
                else if(t[i].status=="rejected"){(g.rejected).push(t[i])}
            }
            this.ticketGroup = g
        }

    }
  }

  </script>

  <style>
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@500&family=Prompt:wght@500&display=swap');
  .dragFont{
    font-family: 'IBM Plex Sans Thai', sans-serif !important;
  }

  .dragArea{
    height: 1050px !important;
  }
  .dragInnerArea{
    height: 900px !important;
  }
  .column-width {
    min-width: 320px;
    width: 320px;
  }
  .ghost-card {
    opacity: 0.5;
    background: #F7FAFC;
    border: 1px solid #4299e1;
  }
  .ticketCard {
    opacity: 0.5;
    background: #F7FAFC;
    border: 1px solid #4299e1;
  }
  .barcode {
		left: 50%;
		box-shadow: 1px 0 0 1px, 5px 0 0 1px, 10px 0 0 1px, 11px 0 0 1px, 15px 0 0 1px, 18px 0 0 1px, 22px 0 0 1px, 23px 0 0 1px, 26px 0 0 1px, 30px 0 0 1px, 35px 0 0 1px, 37px 0 0 1px, 41px 0 0 1px, 44px 0 0 1px, 47px 0 0 1px, 51px 0 0 1px, 56px 0 0 1px, 59px 0 0 1px, 64px 0 0 1px, 68px 0 0 1px, 72px 0 0 1px, 74px 0 0 1px, 77px 0 0 1px, 81px 0 0 1px, 85px 0 0 1px, 88px 0 0 1px, 92px 0 0 1px, 95px 0 0 1px, 96px 0 0 1px, 97px 0 0 1px, 101px 0 0 1px, 105px 0 0 1px, 109px 0 0 1px, 110px 0 0 1px, 113px 0 0 1px, 116px 0 0 1px, 120px 0 0 1px, 123px 0 0 1px, 127px 0 0 1px, 130px 0 0 1px, 131px 0 0 1px, 134px 0 0 1px, 135px 0 0 1px, 138px 0 0 1px, 141px 0 0 1px, 144px 0 0 1px, 147px 0 0 1px, 148px 0 0 1px, 151px 0 0 1px, 155px 0 0 1px, 158px 0 0 1px, 162px 0 0 1px, 165px 0 0 1px, 168px 0 0 1px, 173px 0 0 1px, 176px 0 0 1px, 177px 0 0 1px, 180px 0 0 1px;
		display: inline-block;
		transform: translateX(-90px);
	}
  </style>
