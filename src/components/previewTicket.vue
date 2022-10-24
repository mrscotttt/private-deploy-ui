<template> 
  <v-dialog v-model="previewDialog" width="650" height="500" class="rounded-3xl dragFont">
    <template v-slot:activator="{ on, attrs }">
      <a @click="changeDialog(true)" class="w-8 h-8 mr-4" v-bind="attrs" v-on="on" >
        <font-awesome-icon class="w-8 h-8 text-teal-500" icon="fa-solid fa-eye" />
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
                  <h2 class="text-s font-bold">Ticket Preview</h2>
                </div>
                <button @click="changeDialog(false)" class="ml-auto p-2 bg-rose-700 hover:bg-sky-700 rounded-md text-white">Close</button>
              </div>
              <div class="border-b border-dashed border-b-2 my-5"></div>
              <div class="items-center">
                <div class="grid grid-cols-1 gap-2">
                  <div class="p-4">
                    <div class="ml-auto text-gray-300">Id : {{parentmessage.ticketId}}</div>
                    <div class="text-sm mt-4">Title</div>
                    <div class="text-s font-bold">{{parentmessage.title}}</div>
                    <div class="text-sm mt-4">Description</div>
                    <div class="text-s font-bold">{{parentmessage.description}}</div>
                    <div class="text-sm mt-4">Status</div>
                    <div class="text-s font-bold">{{parentmessage.status}}</div>
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
                      <div class="text-s font-bold">{{parentmessage.contact.name}}</div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Student ID</div>
                      <div class="text-s font-bold">{{parentmessage.contact.studentId}}</div>
                    </div>
                  </div> 
                </div>

                <div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Faculty</div>
                      <div class="text-s font-bold">{{parentmessage.contact.faculty}}</div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Major</div>
                      <div class="text-s font-bold">{{parentmessage.contact.major}}</div>
                    </div>
                  </div> 
                </div>

                <div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="p-4">
                      <div class="text-sm">Telephone</div>
                      <div class="text-s font-bold">{{parentmessage.contact.telephone}}</div>
                    </div>
                    <div class="p-4">
                      <div class="text-sm">Year</div>
                      <div class="text-s font-bold">{{parentmessage.contact.year}}</div>
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
  export default {
    name: 'dragTicket',
    props: ['parentmessage'],
    data: () => ({
      previewDialog: false
    }),
    computed: {
        createTime(){
          return moment(this.parentmessage.createTime).format("DD MMM YYYY hh:mm")
        },
        lastUpdate(){
          return moment(this.parentmessage.lastUpdate).format("DD MMM YYYY hh:mm")
        }
    },
    methods: {
        changeDialog(s) {
          this.previewDialog = s
        }
    }

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
