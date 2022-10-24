<template>
  <div class="p-16 dragFont">
      <div class="overflow-y-auto overflow-x-auto rounded-lg dragArea w-full justify-center  p-8 text-black drop-shadow-2xl backdrop-blur-md bg-white/60">
          <div class="grid grid-cols-3 gap-2 mb-8 ">
            <div class="">
              <div class="text-sm mb-2">Filter key</div>
              <select v-model="filterMode" class="text-s font-bold border-2 bg-white shadow-sm p-2 block w-full appearance-none peer">
                <option>Create Time (Old)</option>
                <option>Create Time (New)</option>
                <option>Update Time (Old)</option>
                <option>Update Time (New)</option>
              </select>
            </div>
            <div class="">
              <div class="text-sm mb-2">Status</div>
              <select v-model="statusGroup" class="block w-full appearance-none peer text-s font-bold border-2 bg-white shadow-sm,, p-2">
                <option>all</option>
                <option>pending</option>
                <option>accepted</option>
                <option>resolved</option>
                <option>rejected</option>
              </select>
            </div>
            <div>
              <div class="text-sm mb-2">Search</div>
              <div class="text-s font-bold border-2 shadow-xs">
                <input type="text" class="w-full" v-model="searchKey"></input>
              </div>
            </div>
          </div>

          <v-data-table
              :headers="headers"
              :items="filterTicket"
              :items-per-page="15"
              :search="this.searchKey"
              class="elevation-1"
          >
            <template #[`item.status`]="{ item }">
              <div v-if="item.status=='pending'" class="text-indigo-600  p-2 m-1 w-full ">pending</div>
              <div v-if="item.status=='accepted'" class="text-yellow-600  p-2 m-1 w-full ">accepted</div>
              <div v-if="item.status=='resolved'" class="text-teal-600  p-2 m-1 w-full ">resolved</div>
              <div v-if="item.status=='rejected'" class="text-red-600  p-2 m-1 w-full ">rejected</div>
            </template>

            <template #[`item.contact`]="{ item }">
              <div>Tel : {{item.contact.telephone}}</div>
            </template>

            <template #[`item.action`]="{ item }">
              <div class="flex-inline">
              <previewTicket :parentmessage="item"></previewTicket>
              <addTicket :parentmessage="item"></addTicket>
            </div>
            </template>
          </v-data-table>
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

export default {
  name: 'dragTicket',
  components: {draggable,previewTicket,addTicket,addNewTicket},
  data: () => ({
    previewDialog: false,
    report: [],
    ticketCard: [],
    statusGroup: 'all',
    filterMode: 'Create Time (New)',
    searchKey: '',
    headers: [
          { text: 'Title', value: 'title',width: '20%',sortable: false, },
          { text: 'Description', value: 'description',width: '20%',sortable: false, },
          { text: 'Create On',align: 'start',sortable: false, value: 'createTimeFormat',width: '10%'},
          { text: 'Last Update', value: 'lastUpdateFormat',width: '10%',sortable: false, },
          { text: 'status', value: 'status',width: '10%',sortable: false, },
          { text: 'Contact', value: 'contact',width: '10%',sortable: false, },
          { text: 'Action', value: 'action',width: '10%',sortable: false,},
        ],
  }),
  created: async function(){
      await this.hookticket()
  },
  computed: {
      filterTicket(){
        let demo = []
        if(this.statusGroup=="all"){
            demo=this.ticketCard
        }
        else{
          (this.ticketCard).forEach((item=>{
            if(item.status==this.statusGroup){
              demo.push(item)
            }
          }))
        }
        
        if(this.filterMode=="Create Time (Old)"){demo.sort((a, b) => a.createTime - b.createTime);}
        if(this.filterMode=="Create Time (New)"){demo.sort((a, b) => b.createTime - a.createTime);}
        if(this.filterMode=="Update Time (Old)"){demo.sort((a, b) => a.lastUpdate - b.lastUpdate);}
        if(this.filterMode=="Update Time (New)"){demo.sort((a, b) => b.lastUpdate - a.lastUpdate);}

        return demo
      }


  },
  methods: {
      async hookticket() {
          try{
              let tkt = await axios.get('/ticket')
              this.ticketCard = tkt.data.Items
              if(this.ticketCard.length>0){this.ticketCard.sort((a, b) => b.createTime - a.createTime);}
          }
          catch(err){
              this.ticketCard = []
          }
      },

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
table {
	//border-collapse: collapse;
	width: 100%;
   max-width: 100%;
   table-layout: fixed !important;
   border-collapse:separate;
   border:solid white 1px;
   border-radius: 8px;
}
.employee-Payroll-table{
	img{
		width: 30px;
		height:30px;
	}
}
.v-data-table table{
   thead,
   tbody,
   tfoot {
      tr {
         td {
            vertical-align: middle;
            font-size: 13px !important;
            font-weight: 400 !important;
            line-height: 20px !important;
            color: rgba(0, 0, 0, 0.87) !important;
            height: 3.75rem  !important;
            border-bottom:0 !important;
         }
         th {
            vertical-align: middle;
            font-size: 14px !important;
            font-weight: 600;
            line-height: 20px !important;
            color: rgba(0, 0, 0, 0.87) !important;
            height: 3.75rem  !important;
            border-bottom:0 !important;
         }
         th.text-center{
            text-align: left !important;
         }
      }
   }
   tr {
      border: none !important;
   }
   thead {
      tr {
         background-color: $base-light;
         th{
            font-weight: 500;
         }
      }
   }
   tbody {
      tr:nth-child(even) {
         background-color: $base-light;
      }
   }
}

@media (max-width: 768px) and (min-width: 320px) {

   table{
      tbody tr td{
         font-size:0.875rem;
      }
	}
	.v-data-table-header-mobile__wrapper{
		width:90px;
	}
}

.table-responsive{
	display: block;
	width: 100%;
	overflow-x: scroll !important;
}
</style>
