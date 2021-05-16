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


- Τα εργαλεια που χρησιμοποισα και θα χρειστουν για την υλοποίηση της άσκησης είναι:
- Το docker desktop
- Το postman
- Το mongo-shell and mongo compass 
- Το VScode

 ~ Παρακάτω θα εξηγήσουμε/αναλύσουμε τα 9 endpoint της άσκησης που υπάρχουν εσωτερικά στο αρχείο app.py
 
1) endpoint: Στο πρώτο ερώτημα ουσιαστικά ειναι να φτίαξουμε ένα function το οπολιο ονομάζεται create_user(): το οποίο το καλούμε μέσω του postman όπου εκει βάζουμε στο localhost5000:///createUser όπως και αντίστοιχα το ίδιο επίσης γίνεται και στα υπόλοιπα endpoint αλλα αντι για  createUser βάζουμε το αντίστοιχο του.
εκέι πέρα απο τα κλασικά checks που γίνονται δηλαδη αν το body είναι σωστό αν δεν έχει κάποια σφάλματα και αν το data περιέχει το username και το password αυτο που κάνουμ είναι ,  να ελέγχουμε αν το data το οποίο το έχουμε περάσει στο username υπάρχει ήδη στην βάση αυτο γίνεται με την συνθήκη if kai count() > 0:


2) Εδώ έχουμε κάτι αντίστοιχο όμως με το login δηλαδή ελέγχουμε πάλι με βάση το κωδικα μασ και αυτα που έχουμε το json αρχείο μας αν το request περιέχει το name και το password και , στη συνέχεια κάνω ένα check που λέει αν το username και το password υπάρχουν μέσα σε ένα απο τα entries τότε κάνει generate το uuid το οποίο το κάνω μέσω της ήδη υπάρχων function που δίνεται, και το επιστρέφει μέσω το json.dumps .Οπου αυτο ουσιαστκά επιστρέφει το result σε μορφή json αν και στην προκειμένη φάση το (res) είναι ένα dictionary.Εάν το username και το password είναι σωστό πεταέι σφάλμα με error 400


3) Στο get student εδω η διαφορά είναι οτι χρειάζετε να περνάμε και το uuid μαζί --> εννοώντας στα headers όμως.Εδω θα λέγαμε οτι αυτο ειναι αρκετά έξυπνο και πιστεύω δύσκολο να το παραποιηση κάποιος hacker ή οποιοςδήποτε.Εδώ πάλι όπως έχουμε πει και παραπάνω ελέγχει αν το json είναι σωστό και αν περιέχει το email.Αν δεν το περιέχει τότε πετάει το error information incomplete που σημάινει ότι , δεν έχει email δεν έχει αυτο που θέλει η βάση.Τότε εκέι βάζουμε το if_session_valid που πρακτικά ελέγχει αν το uuid υπάρχει στη λίστα με τα uuids που έχουν γίνει confirmed (γενικά το uuid γίνεται generate απο τη create_session() η οποία εισάγει το uuid του χρήστησε ένα dictionary με uuids).Τώρα αν βγάλουμε κάποιο λάθος uuid στο header θα μας πετάξει error : user not verifed , με status=401.

4) Στο '/getStudents/thirties' επίσης ελέγχει αν δεν υπάρχει πετάει error αν υπάρχει σημαίνει οτι είναι verifed άρα προχωράει παρακάτω.Καθώς επίσης εδω αυτο που κάνουμε είναι να πάρουμε μια λίστα με όλους τους φοιτητές που έχουν ημ.γεννησης το 1991 , αρχικοποιούμε μια λίστα και μια μεταβλητη c οπου πρακτικα την χρησιμοποιώ σαν counter.Εκεί έχουμε το try except αυτο το έχω βάλει γιατί να μπορούμε εύκολα και απλά να κάνουμε exit απο την while σε περίπτωση ατέρμονου βρόχου.

5) Στο '/getStudents/oldies' εδω πρκατικά είναι το ίδιο με επάνω απλα βάζουμε το {"$lt": 1991}}) δηλαδή less than (πηγή : stackoverflow ) για να βρούμε/επιστέψει του φοιτητες που είναι τουλάχιστον 30 ετών.


6) Στο '/getStudentAddress' κάνουμε επίσης τους ελέγχους που αναφέραμε και πιο πάνω απλα η μόνη διαφορά είναι οτι ελέγχω αν υπάρχει student με αυτο το email προφανώς και επιστρέφουμε το email του και το adreess του.Εαν δεν υπάρχει το email και το adreess αυτο τότε το result δεν υπα΄ρχει 


7) Στο '/deleteStudent' επίσης κάνουμε τα check όπως και παραπάνω , στο ( if not student == None: ) αυτο που κάνω είναι να ελέγχω αν υπάρχει ο φοιτητής και αν υπάρχει να τον κάνει delete  καθώς επίσης φτιάχνω ενα message --> msg το έχω ονομάσει εγώ. Το οποίο εμφανίζε student -------  was deleted. Αλλίως αν δεν υπαρχει ο συγκεκριμένος φοιτητής εμφανίζει το μήνυμα USER NOT VERIFIED με status=401

8) Στο '/addCourses' προφανώς τα ίδια με παραπάνω στο κομμάτι του ελέγχου  και μετα στον έλεγχο ( if not student == None: ) ουσιαστικά  σετάρουμε τα  courses δηλαδή φτιάχνουμε ένα set αντικείμενο θεωρητικά μεταβλητή είναι, αν και --> αυτο που κάνει συγκεκριμένα το function  στο update_one είναι οτι πρακτικα τους λες οτι θέλω να κάνεις update αυτον που έχει το email που θα της δώσουμε και να κάνουμε set τα courses δηλαδή να κάνουμε set τα data που έχω παρει απο το body του request και να το περάσω σε μία key σε έν α κλειδί σε ένα entry που λέγεται courses η μοναδικότητα με το set είναι ότι αν υπάρχει ήδη το κλειδί το κάνει ουσιαστικά update αλλιως αν δεν υπάρχει το κάνει set. Στη συνέχει όταν γίνει αυτό προφανώς θα γίνει successful το request με status=200 , διαφορετικά αν δεν υπάρχει το email θα μας εμφανίσει το "THERE IS NO STUDENT WITH THAT EMAIL TRY AGAIN LATER"




--------------------------------------------------------------------(ENGLISH-VERSION)--------------------------------------------------------------------------
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
- 4) VScode

~ Below we will explain / analyze the 9 endpoints of the exercise that exist internally in the app.py file
 
1) endpoint: The first question is to create a function called create_user (): which we call through the postman where we put in localhost5000: /// createUser as well as the same is done in the other endpoints but instead for createUser we put its equivalent.
beyond the classic checks that are done, ie if the body is correct if it does not have any errors and if the data contains the username and password what we do is, to check if the data that we have passed to the username already exists in the database this is done with the condition if kai count ()> 0:


2) Here we have something similar to login, ie we check again based on our code and what we have in our json file if the request contains the name and password and then I do a check that says if the username and password exist in one of the entries then it generates the uuid which I do through the already existing function that is given, and returns it via json.dumps. Where it essentially returns the result in json format although in this case the (res ) is a dictionary. If the username and password are correct it throws an error with error 400


3) In get student here the difference is that you need to pass the uuid together -> meaning in the headers though.Here we would say that this is quite smart and I think it is difficult to falsify it by a hacker or anyone. Here again as we have said above checks if json is correct and if it contains the email. If it does not contain it then throws the error information incomplete which means that, it does not have email does not have what the database wants. in the list of uuids that have been confirmed (generally uuid is generated by create_session () which inserts its uuid into a dictionary with uuids). Now if we make a mistake uuid in the header will throw us error: user not verifed, with status = 401.

4) In '/ getStudents / thirties' it also checks if it does not exist it throws an error if it exists it means it is verifed so it goes below. Also here what we do is to get a list of all the students born in 1991, we initialize a list and a variable c where I practically use it as a counter. There we have the try except I have put it because we can easily and simply exit from while in case of an endless loop.

5) In '/ getStudents / oldies' here it is basically the same as above we just put {"$ lt": 1991}}) ie less than (source: stackoverflow) to find / return students who are at least 30 years old.


6) In '/ getStudentAddress' we also do the checks we mentioned above and the only difference is that I check if there is a student with this email obviously and we return his email and his address. If there is no email and this address then the result does not exist


7) In '/ deleteStudent' we also do the checks as above, in (if not student == None:) what I do is check if there is a student and if there is to delete him as well as I create a message -> I have named it. Which displayed student ------- was deleted. Otherwise if there is no specific student displays the message USER NOT VERIFIED with status = 401

8) In '/ addCourses' obviously the same as above in the control part and then in the control (if not student == None :) we essentially set the courses, that is, we create a set object that is theoretically variable, although -> what it does Specifically, the function in update_one is that you practically tell them that I want to update the one who has the email that we will give her and set the courses, that is, set the data that I have received from the body of the request and pass it to a key to a key in an entry called courses the uniqueness with the set is that if the key already exists it essentially updates it otherwise if it does not exist it does the set. Then when this is done the request with status = 200 will obviously be successful, otherwise if there is no email it will show us "THERE IS NO STUDENT WITH THAT EMAIL TRY AGAIN LATER"
