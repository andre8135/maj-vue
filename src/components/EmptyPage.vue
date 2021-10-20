<template>
	<div class="p-grid">
		<div class="p-col-12">
			<div class="card">
				<div id="app">
					<FullCalendar :options="calendarOptions" />
					<Dialog header="Dialog" v-model:visible="display" :breakpoints="{ '960px': '75vw' }" :style="{ width: '30vw' }" :modal="true">
						<p class="line-height-3 m-0">
							{{ args }}
						</p>
						<template #footer>
							<Button label="Dismiss" @click="close" icon="pi pi-check" class="p-button-secondary" />
						</template>
					</Dialog>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import "@fullcalendar/core/vdom";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
import timeGridPlugin from "@fullcalendar/timegrid";
// import EventService from "../service/EventService";
// import Calendar from "primevue/calendar";
export default {
	components: {
		// 'p-calendar': Calendar,
		FullCalendar,
	},
	data() {
		return {
			args: null,
			display: false,
			calendarOptions: {
				plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin],
				initialView: "dayGridMonth",
				initialDate: "2021-09-30",
				headerToolbar: {
					left: "prev,next today",
					center: "title",
					right: "dayGridMonth,timeGridWeek,timeGridDay",
				},
				editable: true,
				selectable: true,
				selectMirror: true,
				dayMaxEvents: true,
				dateClick: this.handleDateClick,
				locale: "es"
			},
		};
	},
	methods: {
		handleDateClick: function(arg) {
			this.args =  arg.dateStr
			this.display = true;
			console.log("date click! " + arg.dateStr)
		},
		close() {
			this.display = false;
		},
	},
	// data() {
	// 	return {
	// 		options: {
	// 			plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin],
	// 			initialDate: "2017-02-01",
	// 			headerToolbar: {
	// 				left: "prev,next today",
	// 				center: "title",
	// 				right: "dayGridMonth,timeGridWeek,timeGridDay",
	// 			},
	// 			editable: true,
	// 			selectable: true,
	// 			selectMirror: true,
	// 			dayMaxEvents: true,
	// 		},
	// 		events: null,
	// 	};
	// },
	// eventService: null,
	// created() {
	// 	this.eventService = new EventService();
	// },
	// mounted() {
	// 	this.eventService.getEvents().then((data) => (this.events = data));
	// },
};
</script>

<style scoped></style>
