# hospitalschedulingsystem

Contributors : Akash Bagchi   Akshaya Nadathur    Riya Mary Joseph    Sanchitha N G   Shraavya B K

Aim:
To create a hospital appointment scheduling system that can take user requests to create and manage their doctor’s appointments, with the following functionality:
To create new appointments that will prompt the code to look for the next available time slot to accommodate the patient in, considering the nature of the appointment.
To allow for rescheduling of existing appointments if certain criteria are met, and dynamically re-order appointments in new time slots.
To allow for appointment cancellations, and automatic rescheduling of following appointments.


Working:
The schedule:
All the time slots of a given day are represented by elements of a linked list. Each time slot of 30 minutes is numbered sequentially to signify the time of the day. Each slot contains information such as Name of Patient, Type of Appointment and Appointment urgency.
Appointment booking:
When a user wants to book an appointment, their name, appointment type (Consultation/Blood test/ECG/Surgery) and urgency are taken as input by a function. The program then searches through the schedule linearly, until the first available (vacant) time slot is found. The user’s inputs are copied into the slot and the appointment is confirmed.
Rescheduling
To accommodate for rescheduling appointments, a function will search through the schedule using Name as key, and uses a swap function to accomplish the reschedule. 
Rescheduling will only be offered in postponement, whereas preponement will be automatic based on the urgency type; i.e. when a user wants to postpone their appointment, the swap function prioritises later appointments with the ‘urgent’ flag over appointments with a ‘normal’ flag.
Cancellation
Much like rescheduling, cancellation will use the name of the user to find their appointment booking, and delete their information from the list. If any ‘urgent’ appointments follow the cancelled slot, then it is preponed appropriately.
Admin Control
Finally, an admin management function will allow an admin to manually remove an appointment from the schedule, when said time slot has elapsed.

Conclusion:
This mini-project aims to create an efficient and effective system to manage the booking and management of appointments in a structured and methodical manner. By creating a dynamic system which automatically moves more urgent appointments to earlier available time slots, it removes the need for manual intervention from hospital staff, thereby reducing risk of human error. In a healthcare environment, such a system could not only greatly streamline the working of a hospital system, but also potentially save lives by ensuring that urgent appointments are attended to earlier.
Such a system can also be implemented in various other large-scale operations that require streamlined scheduling, such as in an office space, freighting company, airports, banks, law firms etc. 
The functionality and features of the mini-project are implemented using the concepts of Computational Thinking with Python, applying the concepts learned in the course to real-life problems.
