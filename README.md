[Documentation](https://python-mini-project.github.io/Hospital-Schedule-Management-System/)


# Hospital Schedule Management System

###### v1.1-beta.1

_Developed by **Akash Bagchi(ENG19CS0019), Akshaya Nadathur(ENG19CS0024), Riya Mary Joseph(ENG19CS0258), Sanchitha N G(ENG19CS0281) and Shraavya B K(ENG19CS0300)** for the Computational Thinking with Python Mini Project at Dayananda Sagar University, Kudlu Gate_

This is a schedule management system designed for modern hospitals to use as a next-day appointment booking and management application, assigning appointments to patients based on their preferences as well as allowing for cancellation and dynamic(automatic) rescheduling.
Our code employs the implementation of linked lists using classes and methods in python, as well as several python3 modules such as pandas and tkinter to create a fully functioning and intuitive scheduling system with rudimentary GUI.

## Why linked lists?

We chose linked lists over arrays for the following reasons:

1.	A linked list allows sequential access to its elements which is helpful for scheduling and rescheduling system.
2. Elements can be added to linked list indefinitely whereas an array will get filled or has to be resized. 
3.	In a linked list, new elements can be stored anywhere in the memory.
4.	 Elements in linked list can be easily inserted or removed without reallocation or reorganization of the entire structure because the data items need not be stored continously in memory whereas removing elements from an array leaves empty spaces that are a waste of computer memory. 
5.	In case of linked list, a new element is stored at the first free and available memory location, with only a single overhead step of storing the address of memory location in the previous node of linked list. 
6.	Therefore, operations like insertion and deletion in Linked lists are fast.  
7.	Linked lists are dynamic and flexible and can expand and contract its size.


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

## Analysis - Patient attendance & dealing with no-shows

The analysis file contains graphical representations of the number of people who did not show up for appointments for a provided hypothetical set of data. The data has been made in a way so as to satisfy research results on the same. For example, research tells us that around 42% of people do not show up to appointments, and our data follows the same as well, along with several other key factors which are looked into in graphical form.

![](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/docs/pie.png)

Results:
As patients who do not maintained scheduled times have a negative impact on patient care, productivity and learning opportunities, it is important to understand why this happens in the first place. Refer to our [Graphical analysis](https://github.com/Python-mini-project/Hospital-Schedule-Management-System/blob/main/analysis_1.ipynb) for a detailed univariate and bivariate analysis using Matplot lib and Seaborn which explain the factors that affect patients. 
The main affecting factors turn out to be as follows. People of lower economic status, younger age and unclear schedules are the least likely to show up because they reconsider spending on facilities (eg transport), and do not consider their appointment to be of urgency when personal schedules come in the way. The same goes for people whose appointments are of shorter duration as since it’s a short amount of time, it would be ignored for later. Whereas, if a person were to get a surgery done, he is unlikely to ignore his appointment. 

### Scope for an overbooking system:

While the strategy of overbooking appointments to allow for anticipated non-attendance may be counterproductive for what is supposed to be a scheduling system, it is still a highly recommended try-out. 
A possible implementation of an overbooking model for scheduling arrivals at a medical facility under no-show behavior, with patients having different no-show probabilities and different weights could be done. The scheduler has to assign the patients to time slots in such a way that she minimizes the expected weighted sum of the patients' waiting times and the doctor's idle time and overtime. We first consider the static problem, where the set of patients to be scheduled and their characteristics are known in advance. We partially characterize the optimal schedule and introduce a new sequencing rule that schedules patients according to a single index that is a function of their characteristics. Then we apply our theoretical results and conclusions from numerical experiments to sequential scheduling procedures. We propose a solution to the sequential scheduling problem, where requests for appointments come in gradually over time and the scheduler has to assign each patient to one of the remaining slots that are available in the schedule for a given day. We find that the no-show rate and patients' heterogeneity have a significant impact on the optimal schedule and should be taken under consideration.

### Other possible enhancements to deal with patient no-shows:

Rather than a hypothetical set of data like in the ‘analysis’ function, it is a better option to take real data of patient characteristics and their attendance details in the future. An exploratory data analysis (EDA) beyond just a univariate/bivariate analysis (which is shown in the project) can be performed on the same, which will provide us with a final set of data to use in building a ‘predictive model’ in Python. This could be using libraries in Python such as Logistic Regression, Random Forest Classifier, Decision Tree, KMeans and many more. Once the models are built, the accuracy of each model could be derived from them, and the best predictive model could be decided upon. 
The predictive model results could then be used to come up with solutions for the hospital administration to take physical measures to prevent no-shows by patients.
Another included feature could be a notifying system to remind patients of their confirmed/rescheduled appointments by implementing a Whatsapp API, which is discussed in detail below.

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
