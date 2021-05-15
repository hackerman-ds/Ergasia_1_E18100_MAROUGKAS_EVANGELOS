# Ergasia_1_E18100_MAROUGKAS_EVANGELOS

# Presentation of the student "MAROUGKAS_EVANGELOS" student of digital systems at the University of Piraeus with university professors:@csymvoul and @jdtotow.

Πληροφορίες εργασίας:

Στη καρτέλα εργασίες, στην εργασία «1η υποχρεωτική εργασία 2021» θα βρείτε ένα zip αρχείο που περιέχει μέσα το αρχείο app.py καθώς και το αρχείο students.json.   
Στο αρχείο app.py υπάρχουν 9 συνολικά endpoint τα οποία καλείστε να υλοποιήσετε.
Για το κάθε endpoint υπάρχει αναλυτική περιγραφή στην συνάρτηση που το υλοποιεί. 
Η διαδικασία ανάθεσης των δεδομένων που περνάνε στο body του request κάθε φορά έχει ήδη υλοποιηθεί. Τα δεδομένα κάθε φορά περνάνε σε μία μεταβλητή που ονομάζεται data. 
Το μόνο που χρειάζεται να υλοποιήσετε είναι τα query στη MongoDB, την λήψη ενός uuid από το header του request, καθώς και τη κλήση των ανάλογων συναρτήσεων για την αυθεντικοποίηση του χρήστη. 
Για τον έλεγχο της υλοποίησης θα πρέπει να δημιουργήσετε ένα container MongoDB το οποίο θα ονομάσετε mongodb και θα έχει ακούει στη port 27017 του host.

Έπειτα, θα πρέπει να περάσετε μέσα τα δεδομένα που υπάρχουν στο αρχείο students.json. ΠΡΟΣΟΧΗ: Θα πρέπει πρώτα να αντιγράψετε τα αρχεία στο container και μετά με τη χρήση της εντολής mongoimport να τα περάσετε σε ένα collection με όνομα Students της ΒΔ InfoSys. 





---------------------------------------------------------------------(ENGLISH-VERSION)------------------------------------------------------------------------------------------
- Working information:

In the Tasks tab, in the task "1st compulsory homework 2021" you will find a zip file containing the app.py file as well as the students.json file.
In the app.py file there are 9 total endpoints which you are called to implement.
For each endpoint there is a detailed description in the function that implements it.
The process of assigning the data that passes to the body of the request each time has already been implemented. The data each time passes to a variable called data.
All you need to do is query the MongoDB, download a uuid from the request header, and call the corresponding functions to authenticate the user.
To control the implementation you need to create a MongoDB container which you will name mongodb and it will listen on port 27017 of the host.

Next, you need to enter the data in the students.json file. ATTENTION: You must first copy the files to the container and then using the mongoimport command to pass them to a collection named Students of NW InfoSys.


- In this project we use the tools: 
- 1) docker desktop 
- 2) postman 
- 3) mongo-shell and mongo-compass
- 4)VScode


