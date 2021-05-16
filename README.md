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


