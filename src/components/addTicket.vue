<template>
  <v-dialog v-model="previewDialog" width="650" height="500" class="rounded-3xl dragFont">
    <template v-slot:activator="{ on, attrs }">
      <a @click="changeDialog(true)" class="w-8 h-8 mr-4" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="w-8 h-8 text-yellow-500" icon="fa-solid fa-pen-to-square" />
      </a>
    </template>
    <div class="w-full h-full mx-auto bg-gray-300 dragFont">
      <div class="flex flex-col">
        <div class="bg-white relative drop-shadow-2xl   p-4 m-4">
          <div class="flex-none sm:flex">
            <div class=" relative h-32 w-32   sm:mb-0 mb-3 hidden">
              <a href="#"
                class="absolute -right-2 bottom-2   -ml-3  text-white p-1 text-xs bg-green-400 hover:bg-green-500 font-medium tracking-wider rounded-full transition ease-in duration-300">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"
                  class="h-4 w-4">
                  <path
                    d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z">
                  </path>
                </svg>
              </a>
            </div>
            <div class="flex-auto justify-evenly">
              <div class="flex items-center justify-between">
                <div class="flex items-center  my-1">
                  <span class="mr-3 rounded-full bg-white w-8 h-8"></span>
                  <h2 class="text-s font-bold">Ticket Update</h2>
                </div>
                <div v-if="load" class="ml-auto mr-2 p-2">
                  <svg class="animate-spin h-5 w-5 mr-3" viewBox="0 0 24 24">
                  </svg>
                </div>
                <button @click="save()" class="ml-auto mr-2 p-2 bg-indigo-700 hover:bg-yellow-700 rounded-md text-white">Save</button>
                <button @click="changeDialog(false)" class="ml-auto p-2 bg-red-500 hover:bg-yellow-700 rounded-md text-white">Close</button>
              </div>
              <div class="border-b border-dashed border-b-2 my-5"></div>
              <div class="items-center">
                <div class="grid grid-cols-1 gap-2">
                  <div class="p-4">
                    <div v-if="warning" class="ml-auto text-red-300">Not correct, Please check your input.</div>
                    <div class="ml-auto text-gray-300">Id : {{editTicket.ticketId}}</div>
                    <div class="text-sm mt-4">Title</div>
                    <div class="text-s font-bold border-2 shadow-2xl">
                      <input type="text" class="w-full" v-model="editTicket.title"></input>
                    </div>
                    <div class="text-sm mt-4">Description</div>
                    <div class="text-s font-bold border-2 shadow-2xl">
                      <textarea class="w-full h-auto overflow-y-auto overflow-x-auto p-2" v-model="editTicket.description"></textarea>
                    </div>
                    <div class="text-sm mt-4">Status</div>
                    <div class="text-s font-bold border-2 shadow-2xl p-2">
                      <select v-model="editTicket.status" class="block w-full appearance-none peer">
                        <option  v-for="(element, index) in statusSelect" >{{element}}</option>
                      </select>
                    </div>
                  </div>
                </div>
                </div>
                <div class="border-b border-dashed border-b-2 my-5 pt-5">
                  <div class="absolute rounded-full w-5 h-5 bg-gray-300 -mt-2 -left-2"></div>
                  <div class="absolute rounded-full w-5 h-5 bg-gray-300 -mt-2 -right-2"></div>
                </div>
                <div>
                  <div class="ml-auto text-gray-300">Contact</div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Name</div>
                      <div class="text-s font-bold border-2 shadow-2xl">
                        <input type="text" class="w-full" v-model="editTicket.contact.name"></input>
                      </div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Student ID</div>
                      <div class="text-s font-bold border-2 shadow-2xl">
                        <input type="text" class="w-full" v-model="editTicket.contact.studentId"></input>
                      </div>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Faculty</div>
                      <div class="text-s font-bold border-2 shadow-2xl p-2">
                        <select v-model="editTicket.contact.faculty" class="block w-full appearance-none peer">
                          <option  v-for="(element, index) in facultySelect" >{{element}}</option>
                        </select>
                      </div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Major</div>
                      <div class="text-s font-bold border-2 shadow-2xl">
                        <input type="text" class="w-full" v-model="editTicket.contact.major"></input>
                      </div>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Telephone</div>
                      <div class="text-s font-bold border-2 shadow-2xl">
                        <input type="text" class="w-full" v-model="editTicket.contact.telephone"></input>
                      </div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Year</div>
                      <div class="text-s font-bold border-2 shadow-2xl p-2">
                        <select v-model="editTicket.contact.year" class="block w-full appearance-none peer">
                          <option  v-for="(element, index) in yearSelect" >{{element}}</option>
                        </select>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="border-b border-dashed border-b-2 my-5 pt-5">
                  <div class="absolute rounded-full w-5 h-5 bg-gray-300 -mt-2 -left-2"></div>
                  <div class="absolute rounded-full w-5 h-5 bg-gray-300 -mt-2 -right-2"></div>
                </div>
                <div>
                  <div class="ml-auto text-gray-300">Time</div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Create On</div>
                      <div class="text-s font-bold">{{createTime}}</div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Last Update</div>
                      <div class="text-s font-bold">{{lastUpdate}}</div>
                    </div>
                  </div>
                </div>
                </div>
              </div>
            </div>
          </div>
        </div>
    </div>
</v-dialog>
</template>

  <script>
  import moment from 'moment';
  import axios from 'axios';
  export default {
    name: 'dragTicket',
    props: ['parentmessage'],
    data: () => ({
      previewDialog: false,
      statusSelect: ["pending","accepted","resolved","rejected"],
      yearSelect: [1,2,3,4,5,6,7,8,"จบการศึกษา"],
      facultySelect: ["คณะเกษตร","คณะบริหารธุรกิจ",
      "คณะประมง","คณะมนุษยศาสตร์","คณะวนศาสตร์","คณะวิทยาศาสตร์","คณะวิศวกรรมศาสตร์","คณะศึกษาศาสตร์",
      "คณะเศรษฐศาสตร์","คณะสถาปัตยกรรมศาสตร์","คณะสังคมศาสตร์","คณะสัตวแพทยศาสตร์",
      "คณะอุตสาหกรรมเกษตร","คณะเทคนิคการสัตวแพทย์","คณะสิ่งแวดล้อม",],
      editTicket: [],
      load: false,
      warning: false
    }),
    computed: {
        createTime(){
          return moment(this.editTicket.createTime).format("DD MMM YYYY hh:mm")
        },
        lastUpdate(){
          return moment(this.editTicket.lastUpdate).format("DD MMM YYYY hh:mm")
        },
        sct(){
          return ["pending","accepted","resolved","rejected"]
        },
        validateitem(){
          if(
            this.editTicket.title &&
            this.editTicket.description &&
            this.editTicket.contact.name &&
            this.editTicket.contact.studentId &&
            this.editTicket.contact.telephone &&
            this.editTicket.contact.faculty &&
            this.editTicket.contact.major
          ){
            return true
          }
          else{
            return false
          }
        }
    },
    methods: {
        changeDialog(s) {
          this.previewDialog = s
          this.hookticket()
        },
        async hookticket() {
            try{
                let url = "/ticketById/"+this.parentmessage.ticketId+"/"+this.parentmessage.createTime
                let tkt = await axios.get(url)
                this.editTicket = tkt.data.Item
            }
            catch(err){
                this.editTicket = []
            }
        },
        async save() {
            // console.log("save")
            this.load = true
            if(!this.validateitem){
              this.load = false
              this.warning = true
            }
            else{
              this.warning = false
              try{
                let tkt = await axios.post('/addTicket',this.editTicket)
                // console.log("save success")
                this.load = false
                this.previewDialog = false
                location.reload()
              }
              catch(err){
                this.load = false
                // console.log("save fail",err)
              }
            }

        }
    },
    created: async function(){
        await this.hookticket()
    },

  }
  </script>

  <style>
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@500&family=Prompt:wght@500&display=swap');
  .dragFont{
    font-family: 'IBM Plex Sans Thai', sans-serif !important;
  }
  .barcode {
		left: 50%;
		box-shadow: 1px 0 0 1px, 5px 0 0 1px, 10px 0 0 1px, 11px 0 0 1px, 15px 0 0 1px, 18px 0 0 1px, 22px 0 0 1px, 23px 0 0 1px, 26px 0 0 1px, 30px 0 0 1px, 35px 0 0 1px, 37px 0 0 1px, 41px 0 0 1px, 44px 0 0 1px, 47px 0 0 1px, 51px 0 0 1px, 56px 0 0 1px, 59px 0 0 1px, 64px 0 0 1px, 68px 0 0 1px, 72px 0 0 1px, 74px 0 0 1px, 77px 0 0 1px, 81px 0 0 1px, 85px 0 0 1px, 88px 0 0 1px, 92px 0 0 1px, 95px 0 0 1px, 96px 0 0 1px, 97px 0 0 1px, 101px 0 0 1px, 105px 0 0 1px, 109px 0 0 1px, 110px 0 0 1px, 113px 0 0 1px, 116px 0 0 1px, 120px 0 0 1px, 123px 0 0 1px, 127px 0 0 1px, 130px 0 0 1px, 131px 0 0 1px, 134px 0 0 1px, 135px 0 0 1px, 138px 0 0 1px, 141px 0 0 1px, 144px 0 0 1px, 147px 0 0 1px, 148px 0 0 1px, 151px 0 0 1px, 155px 0 0 1px, 158px 0 0 1px, 162px 0 0 1px, 165px 0 0 1px, 168px 0 0 1px, 173px 0 0 1px, 176px 0 0 1px, 177px 0 0 1px, 180px 0 0 1px;
		display: inline-block;
		transform: translateX(-90px);
	}
  </style>
