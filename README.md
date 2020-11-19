[Documentation](https://python-mini-project.github.io/Hospital-Schedule-Management-System/)


# Hospital Schedule Management System

###### v1.1-beta.1

_Developed by **Akash Bagchi, Akshaya Nadathur, Riya Mary Joseph, Sanchitha N G and Shraavya B K** for the Computational Thinking with Python Mini Project at Dayananda Sagar University, Kudlu Gate_

This is a schedule management system designed for modern hospitals to use as a next-day appointment booking and management application, assigning appointments to patients based on their preferences as well as allowing for cancellation and dynamic(automatic) rescheduling.
Our code employs the implementation of linked lists using classes and methods in python, as well as several python3 modules such as pandas and tkinter to create a fully functioning and intuitive scheduling system with rudimentary GUI.

## Functionality:

1. Appointment Creation
   - Different Schedules for different doctors (eg: X-Rays are handled by the radiologist whereas minor surgeries are handled by the General surgeon.)
   - Mechanisms in place to prevent overwriting of existing appointments by new ones
   - User is given the choice to opt-in for automatic rescheduling
   - Appointment confirmed acknowledgement messages to verify succesful booking
2. Appointment Viewing
   - Any user can review their appointment details simply by entering their contact information as a search parameter.
3. Appointment Cancellation
   - User can cancel their appointment by entering their details.
   - Automatic Rescheduling: Upon cancellation, the schedule is scanned for following appointments that have opted-in for automatic rescheduling. Should such an appointment be encountered that can be accomodated in the number of slots freed by the cancellation, it is automatically moved to the earlier time, and the old times are made available for bookings once more.
4. Admin View
   - Enabled mechanism for hospital staff to access password-protected view of all staff member's schedules, to ensure there is no confusion, and to facilitate manual cancellation by hospital staff in case of disparity or errors (negligible probability).

## Working - Backend

### The Schedule

Our schedule for this system considers a 12-hour working day in a hospital, comprised of 24 half-hour time slots. The Class _node_ is used to create the basic data structure for any one appointment slot, containing the patient's name, contact information, appointment details, timeslot (position in schedule) and link to the next node. The class **linked_list** is then used to envelop several of these _nodes_ in a list structure which when initialized, forms the schedule

```python
class node:
    def __init__(self, timeslot=None, Name = None, Contact_number = None, Type = None, Reschedule = None):
        self.timeslot=timeslot
        self.Name = Name
        self.Contact_number = Contact_number
        self.Type = Type
        self.Reschedule = Reschedule
        self.next = None

class linked_list:
    def __init__(self):
        self.head = node()

#Initialising schedules for the doctors, and creating 24 empty timeslots in each

physician_schedule=linked_list()
gensurgeon_schedule=linked_list()
radiologist_schedule=linked_list()

for i in range(24):
    physician_schedule.append(i+1, None, None, None, None)
    gensurgeon_schedule.append(i+1, None, None, None, None)
    radiologist_schedule.append(i+1, None, None, None, None)
```

### Appointment Creation

The "appointment_details_primaryinput" function takes in the user's Name, Contact information and desired appointment type. Based on type, the user is shown all the unoccupied timeslots of the appropriate doctor's schedule, accounting also for the size of their desired appointment type, to ensure that an appointment doesn't accidentally overwrite another appointment slot, or try to exceed the schedule's total size of 24 slots.
The user is also asked for their automatic rescheduling preferences, which will determine if their appointment is dynamically moved to earlier times that can accomodate them, should any open up.

```python
#Appointment creation function:
#Takes input of appointment request details from user, and moves the same into appropriate doctor's schedule

def appointment_details_primaryinput():
    Name = input("Full Name:")
    
    Contact_number = input("Contact Number:")
.
.
.
```

The script then uses the "insert_new_appointment" and "appointmentconfirmed_acknowledge" methods to update the respective doctor's schedule with the new appointment.

```python
def insert_new_appointment(self, timeslot, Name, Contact_number, Type, Reschedule):
        cur_node = self.head
        while cur_node.next != None:
            cur_node=cur_node.next
            if cur_node.timeslot == timeslot:
                cur_node.Name = Name
                cur_node.Contact_number = Contact_number
                cur_node.Type = Type
                cur_node.Reschedule = Reschedule
```

<img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/createapp.PNG" style="zoom:80%;" />



### Appointment Cancellation

The "appointment_deletion_input" function takes all relevant information from the user and calls the "delete_appointment" method to scan through the appropriate schedule for the right slots, and empty the same. The method then makes all the timeslots previously occupied by said appointment available for booking again, to ensure that time is not wasted in the working day.

Further, the method calls the "reschedule_appointment" method when working is complete, to dynamically reschedule any following appointments wishing for earlier times, granted that it can be accomodated in the newly emptied slots.

```python
def delete_appointment(self, Name, contactn, atype):
        dicttime={1:"9:00",2:"9:30",3:"10:00",4:"10:30",5:"11:00",6:"11:30",7:"12:00",8:"12:30",9:"13:00",10:"13:30",11:"14:00",12:"14:30",13:"15:00",14:"15:30",15:"16:00",16:"16:30",17:"17:00",18:"17:30",19:"18:00",20:"18:30",21:"19:00",22:"19:30",23:"20:00",24:"20:30"}
        cur_node = self.head
        flag = 0
        while cur_node.next != None:
.
.
.

def reschedule_appointment(self, atype, start):
        dicttime={1:"9:00",2:"9:30",3:"10:00",4:"10:30",5:"11:00",6:"11:30",7:"12:00",8:"12:30",9:"13:00",10:"13:30",11:"14:00",12:"14:30",13:"15:00",14:"15:30",15:"16:00",16:"16:30",17:"17:00",18:"17:30",19:"18:00",20:"18:30",21:"19:00",22:"19:30",23:"20:00",24:"20:30"}
        if atype in [1,2,7]: elen = 1
        elif atype in [3,4,5,8]: elen = 2
        else: elen = 6
.
.
.
```

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/deleteapp.PNG)

**Automatic Rescheduling example:**

- Before Cancellation:

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/admin2.PNG)

- After Cancellation:

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/admin3.PNG)



### Admin View

The admin view function enables any logistical hospital staff with the (customizable by hospital) username and password to view the current state of all staff members' schedules.

```python
def admin():
    user="hospital"
    pas="doctor123"
    username=input("Enter username:")
    password=input("Enter password:")
    if username == user and password == pas:
        print("\n\nWelcome, Admin.\n")
        enter()
    else:
.
.
.
```

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/admin1.PNG)

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/admin2.PNG)

## Working - Frontend

The front - end for our program is made possible using the TKinter module, using which we created a rudimentary GUI with buttons for all primary user functions. The front - end code (and thus the scheduling system as a whole) runs until the GUI is closed. This system is designed to always be open on a hospital computer, and refreshed at the start of every working day.

```python
import sys
from tkinter import *
%run backend.ipynb

def term():
    window.destroy()
    sys.exit("Thank you for using our Schedule Management System")

window = Tk()
window.title("Hospital Schedule Management System")
.
.
.
```

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/gui.PNG)

We are currently looking into deployment as a web-application.



## Scope for Integration of APIs:

**Whatsapp API from _twilio_ :**

Using twilio.com 's WhatsApp API, tested out the scope of integration of Whatsapp message notifications for booking/reschedule acknowledgements.

Twilio's Whatsapp API allows for the creation of basic conversational bots. By setting up an account using one's mobile number, twilio provides the user with some ready-to-test templates for functions such as appointment reminders

<img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/whatsapp.PNG" style="zoom: 67%;" />

<img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/IMG_20201104_222050.jpg" style="zoom: 25%;" />

- On pip installing flask and twilio, by creating a Flask web app to run on a local server, we can deploy a basic script to take in an incoming message, and relay it back to the user as confirmation that the API is working. 

  <img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/whatsapp1.PNG" style="zoom:50%;" />

- Since a local server cannot be used as a callback URL for the API, we deploy the same using ngrock cloud services to tunnel from a public URL to our local application.

  <img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/whatsapp2.PNG" style="zoom:50%;" />

  The  script template is as shown

  <img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/whatsapp3.PNG" style="zoom:50%;" />

  Once deployed on a public URL, and set as the Callback URL for our API, we can test the working by sending any message to the bot.

<img src="https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/IMG_20201104_222100.jpg" style="zoom:25%;" />

To fully implement the same into our program, one could further deploy the application on a cloud server service such as *Heroku* to enable the functioning of the API without a Flask and ngrok application running on the host computer. 

Linking the scripts to the back-end of our hospital schedule management system could enable the system to send automated confirmation messages to patients' given contact numbers via Whatsapp in the event of appointment booking, cancellation or rescheduling.

While the full deployment of such a feature using the Whatsapp API from _Twilio_ may not be possible in the given timeframe, the scope for user-friendly functionality is sizeable. By sending out automated confirmation/acknowledgement/reminder messages, the efficiency and intuitiveness of the automated schedule management system would be greatly improved; Reducing risk of patients being unaware or forgetful of their appointment times, especially when automatically rescheduled.



###### [View on github](https://github.com/Python-mini-project/hospitalschedulingsystem)
