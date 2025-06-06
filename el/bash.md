---
contributors:
    - ["Dimitri Kokkonis", "https://github.com/kokkonisd"]
---

Η λέξη «bash» είναι ένα από τα ονόματα του unix shell (τερματικός), το οποίο
διανέμεται επίσης ως προεπιλεγμένος τερματικός για το λειτουργικό σύστημα GNU, τα Linux και τα macOS.
Σχεδόν όλα τα παραδείγματα που ακολουθούν μπορούν να αποτελέσουν μέρος ενός
προγράμματος τερματικού (shell script) ή να εκτελεσθούν απευθείας από τον
τερματικό.

[Διαβάστε περισσότερα εδώ.](http://www.gnu.org/software/bash/manual/bashref.html)

```bash
#!/usr/bin/env bash
# Η πρώτη γραμμή του προγράμματος είναι το shebang που υποδεικνύει στο σύστημα
# πώς να εκτελέσει το πρόγραμμα: http://en.wikipedia.org/wiki/Shebang_(Unix)
# Όπως ήδη θα καταλάβατε, τα σχόλια ξεκινούν με τον χαρακτήρα #. Το shebang
# είναι επίσης ένα σχόλιο.
# ΣτΜ.: Τα ονόματα των μεταβλητών είναι γραμμένα σε greeklish καθώς η Bash δεν
# επιτρέπει την χρήση unicode χαρακτήρων.

# Ένα απλό παράδειγμα τύπου «hello world»:
echo Καλημέρα, Κόσμε! # => Καλημέρα, Κόσμε!

# Κάθε εντολή ξεκινά σε μια νέα γραμμή, ή μετά από ένα ελληνικό ερωτηματικό:
echo 'Αυτή είναι η πρώτη γραμμή'; echo 'Αυτή είναι η δεύτερη γραμμή'
# => Αυτή είναι η πρώτη γραμμή
# => Αυτή είναι η δεύτερη γραμμή

# Ορίζουμε μεταβλητές ως εξής:
Metavliti="Κάποιο αλφαριθμητικό"

# Αλλά όχι ως εξής:
Metavliti = "Κάποιο αλφαριθμητικό" # => επιστρέφει το λάθος
# «Metavliti: command not found»
# Η Bash θα καταλάβει πως η Metavliti είναι κάποια εντολή που πρέπει να
# εκτελέσει και θα επιστρέψει ένα λάθος γιατί δεν μπορεί να την βρει.

# Ούτε έτσι μπορούμε να δηλώσουμε μεταβλητές:
Metavliti= 'Κάποιο αλφαριθμητικό' # => επιστρέφει το λάθος: «Κάποιο
                                  # αλφαριθμητικό: command not found»
# Η Bash θα καταλάβει πως το αλφαριθμητικό «Κάποιο αλφαριθμητικό» είναι μια
# εντολή που πρέπει να εκτελέσει και θα επιστρέψει ένα λάθος γιατί δεν μπορεί
# να την βρει. (Σε αυτή την περίπτωση το τμήμα της εντολής «Metavliti=» θα
# ερμηνευθεί ως ορισμός μεταβλητής ισχύων μόνο στο πλαίσιο της εντολής
# «Κάποιο αλφαριθμητικό».)

# Ας χρησιμοποιήσουμε την μεταβλητή:
echo $Metavliti # => Κάποιο αλφαριθμητικό
echo "$Metavliti" # => Κάποιο αλφαριθμητικό
echo '$Metavliti' # => $Metavliti
# Όταν χρησιμοποιούμε την ίδια την μεταβλητή - είτε είναι για να της δώσουμε
# μια νέα αξία, για να την εξάγουμε ή για οτιδήποτε άλλο - γράφουμε το όνομά
# της χωρίς τον χαρακτήρα $. Αν θέλουμε να χρησιμοποιήσουμε την αξία της
# μεταβλητής, πρέπει να χρησιμοποιήσουμε τον χαρατήρα $.
# Να σημειωθεί πώς ο χαρακτήρας ' δεν θα μετατρέψει τις μεταβλητές στις αξίες
# τους!

# Επέκταση παραμέτρων ${ }:
echo ${Metavliti} # => Κάποιο αλφαριθμητικό
# Αυτή είναι μια απλή χρήση της επέκτασης παραμέτρων.
# Η επέκταση παραμέτρων εξάγει μια αξία από μια μεταβλητή.
# Κατά την επέκταση η τιμή ή η παράμετρος μπορεί να τροποποιηθεί.
# Ακολουθούν άλλες μετατροπές που μπορούν να προστεθούν σε αυτή την επέκταση.

# Αντικατάσταση αλφαριθμητικών μέσα σε μεταβλητές
echo ${Metavliti/Κάποιο/Ένα} # => Ένα αλφαριθμητικό
# Αυτή η τροποποίηση θα αντικαταστήσει την πρώτη εμφάνιση της λέξης «Κάποιο»
# με την λέξη «Ένα».

# Υποαλφαριθμητικό μιας μεταβλητής
Mikos=7
echo ${Metavliti:0:Mikos} # => Κάποιο
# Αυτή η τροποποίηση θα επιστρέψει μόνο τους πρώτους 7 χαρακτήρες της τιμής
# της μεταβλητής.
echo ${Metavliti: -5} # => ητικό
# Αυτή η τροποποίηση θα επιστρέψει τους τελευταίους 5 χαρακτήρες (προσοχή στο
# κενό πριν το -5).

# Μήκος αλφαριθμητικού
echo ${#Metavliti} # => 20

# Προεπιλεγμένη αξία για μια μεταβλητή
echo ${Foo:-"ΠροεπιλεγμένηΑξίαΑνΤοFooΕίναιΑόριστοΉΆδειο"}
# => ΠροεπιλεγμένηΑξίαΑνΤοFooΕίναιΑόριστοΉΆδειο
# Αυτό δουλεύει στην περίπτωση που το Foo είναι αόριστο (Foo=) ή άδειο
# (Foo="")· το μηδέν (Foo=0) επιστρέφει 0.
# Να σημειωθεί πως αυτή η εντολή απλώς επιστρέφει την προεπιλεγμένη αξία και
# δεν τροποποιεί την αξία της μεταβλητής.

# Ορισμός ενός πίνακα με 6 στοιχεία
pinakas0=(ένα δύο τρία τέσσερα πέντε έξι)
# Εντολή που τυπώνει το πρώτο στοιχείο
echo $pinakas0 # => "ένα"
# Εντολή που τυπώνει το πρώτο στοιχείο
echo ${pinakas0[0]} # => "ένα"
# Εντολή που τυπώνει όλα τα στοιχεία
echo ${pinakas0[@]} # => "ένα δύο τρία τέσσερα πέντε έξι"
# Εντολή που τυπώνει τον αριθμό των στοιχείων
echo ${#pinakas0[@]} # => "6"
# Εντολή που τυπώνει τον αριθμό των χαρακτήρων στο τρίτο στοιχείο
echo ${#pinakas0[2]} # => "4"
# Εντολή που τυπώνει δύο στοιχεία ξεκινώντας από το τέταρτο
echo ${pinakas0[@]:3:2} # => "τέσσερα πέντε"
# Εντολή που τυπώνει όλα τα στοιχεία, το καθένα σε διαφορετική γραμμή
for i in "${pinakas0[@]}"; do
    echo "$i"
done

# Επέκταση αγκίστρων { }
# Χρησιμοποιείται για την παραγωγή αλφαριθμητικών
echo {1..10} # => 1 2 3 4 5 6 7 8 9 10
echo {a..z} # => a b c d e f g h i j k l m n o p q r s t u v w x y z
# Η εντολή θα τυπώσει όλο το εύρος, από την πρώτη μέχρι την τελευταία αξία

# Ενσωματωμένες μεταβλητές
# Υπάρχουν κάποιες χρήσιμες ενσωματωμένες μεταβλητές, όπως:
echo "Η τιμή την οποία επέστρεψε το τελευταίο πρόγραμμα: $?"
echo "Ο αριθμός PID αυτού του script: $$"
echo "Ο αριθμός των παραμέτρων που περάστηκαν σε αυτό το script: $#"
echo "Όλες οι παράμετροι που περάστηκαν σε αυτό το script: $@"
echo "Οι παράμετροι του script διαχωρισμένες σε μεταβλητές: $1 $2..."

# Τώρα που γνωρίζουμε πως να τυπώνουμε (echo) και να χρησιμοποιούμε μεταβλητές,
# ας μάθουμε κάποια από τα υπόλοιπα βασικά στοιχεία της Bash!

# Ο τρέχων κατάλογος (ή αλλιώς, φάκελος) μπορεί να βρεθεί μέσω της εντολής
# `pwd`.
# `pwd` σημαίνει «print working directory».
# Μπορούμε επίσης να χρησιμοποιούμε την ενσωματωμένη μεταβλητή `$PWD`.
# Παρακολουθήστε πως οι δύο εντολές που ακολουθούν είναι ισοδύναμες:
echo "Είμαι στον κατάλογο $(pwd)" # εκτελεί την εντολή `pwd` και τυπώνει το
                                  # αποτέλεσμα
echo "Είμαι στον κατάλογο $PWD" # τυπώνει την αξία της μεταβλητής

# Αν έχετε πολλά μηνύματα στον τερματικό, η εντολή `clear` μπορεί να
# «καθαρίσει» την οθόνη σας
clear
# Η συντόμευση Ctrl-L δουλεύει επίσης όσον αφορά το «καθάρισμα»

# Ας διαβάσουμε μια αξία από κάποια είσοδο:
echo "Πώς σε λένε;"
read Onoma # Προσέξτε πως δεν χρειάστηκε να ορίσουμε μια νέα μεταβλητή
echo Καλημέρα, $Onoma!

# Η δομή των if statements έχει ως εξής:
# (μπορείτε να εκτελέσετε την εντολή `man test` για περισσότερες πληροφορίες
# σχετικά με τα conditionals)
if [ $Onoma != $USER ]
then
    echo "Το όνομά σου δεν είναι το όνομα χρήστη σου"
else
    echo "Το όνομά σου είναι το όνομα χρήστη σου"
fi
# Η συνθήκη είναι αληθής αν η τιμή του $Onoma δεν είναι ίδια με το τρέχον
# όνομα χρήστη στον υπολογιστή

# ΣΗΜΕΙΩΣΗ: Αν το $Onoma είναι άδειο, η Bash βλέπει την συνθήκη ως:
if [ != $USER ]
# το οποίο αποτελεί συντακτικό λάθος
# οπότε ο «ασφαλής» τρόπος να χρησιμοποιούμε εν δυνάμει άδειες μεταβλητές στην
# Bash είναι ο εξής:
if [ "$Onoma" != $USER ] ...
# ο οποίος, όταν το $Onoma είναι άδειο, θα ερμηνευθεί από την Bash ως:
if [ "" != $USER ] ...
# το οποίο και δουλεύει όπως θα περιμέναμε.

# Υπάρχει επίσης η εκτέλεση εντολών βάσει συνθηκών
echo "Εκτελείται πάντα" || echo "Εκτελείται μόνο αν η πρώτη εντολή αποτύχει"
# => Εκτελείται πάντα
echo "Εκτελείται πάντα" && echo "Εκτελείται μόνο αν η πρώτη εντολή ΔΕΝ αποτύχει"
# => Εκτελείται πάντα
# => Εκτελείται μόνο αν η πρώτη εντολή ΔΕΝ αποτύχει


# Για να χρησιμοποιήσουμε τους τελεστές && και || με τα if statements,
# χρειαζόμαστε πολλαπλά ζευγάρια αγκύλων:
if [ "$Onoma" == "Σταύρος" ] && [ "$Ilikia" -eq 15 ]
then
    echo "Αυτό θα εκτελεστεί αν το όνομα ($Onoma) είναι Σταύρος ΚΑΙ η ηλικία ($Ilikia) είναι 15."
fi

if [ "$Onoma" == "Δανάη" ] || [ "$Onoma" == "Ζαχαρίας" ]
then
    echo "Αυτό θα εκτελεστεί αν το όνομα ($Onoma) είναι Δανάη Ή Ζαχαρίας."
fi

# Υπάρχει επίσης ο τελεστής `=~`, που εκτελεί ένα regex πάνω σε ένα
# αλφαριθμητικό:
Email=me@example.com
if [[ "$Email" =~ [a-z]+@[a-z]{2,}\.(com|net|org) ]]
then
    echo "Η διεύθυνση email είναι σωστά διατυπωμένη!"
fi
# Να σημειωθεί πως ο τελεστής `=~` δουλεύει μόνο με διπλές αγκύλες [[ ]],
# που είναι ωστόσο διαφορετικές από τις μονές [ ].
# Δείτε το http://www.gnu.org/software/bash/manual/bashref.html#Conditional-Constructs
# για περισσότερες πληροφορίες σχετικά με αυτό.

# Επαναπροσδιορισμός της εντολής `ping` ως alias (ψευδώνυμο) για την αποστολή 5
# πακέτων
alias ping='ping -c 5'
# Ακύρωση του alias και χρήση της εντολής όπως είναι κανονικά ορισμένη
\ping 192.168.1.1
# Εκτύπωση όλων των aliases
alias -p

# Οι μαθηματικές εκφράσεις ορίζονται ως εξής:
echo $(( 10 + 5 )) # => 15

# Αντίθετα με άλλες γλώσσες προγραμματισμού, η Bash είναι επίσης ένα shell, άρα
# δουλεύει στο πλαίσιο ενός «τρέχοντος καταλόγου». Μπορούμε να δούμε μια λίστα
# αρχείων και καταλόγων στον τρέχων κατάλογο με την εντολή ls:
ls # Τυπώνει μια λίστα των αρχείων και υποκαταλόγων που περιέχονται στον τρέχων
   # κατάλογο

# Αυτή η εντολή έχει επιλογές που ελέγχουν την εκτέλεσή της:
ls -l # Τυπώνει κάθε αρχείο και κατάλογο σε διαφορετική γραμμή
ls -t # Ταξινομεί τα περιεχόμενα του καταλόγου με βάσει την ημερομηνία
      # τελευταίας τροποποίησης (σε φθίνουσα σειρά)
ls -R # Εκτελεί την εντολή `ls` αναδρομικά στον τρέχων κατάλογο και σε όλους
      # τους υποκαταλόγους του.

# Τα αποτελέσματα μιας εντολής μπορούν να μεταβιβαστούν σε μιαν άλλη.
# Η εντολή `grep` φιλτράρει τα δεδομένα που δέχεται βάσει μοτίβων.
# Έτσι, μπορούμε να τυπώσουμε μια λίστα αρχείων κειμένου (.txt) στον τρέχων
# κατάλογο:
ls -l | grep "\.txt"

# Μπορούμε να χρησιμοποιήσουμε την εντολή `cat` για να τυπώσουμε το περιεχόμενο
# ενός ή περισσότερων αρχείων στην προεπιλεγμένη έξοδο (stdout):
cat file.txt

# Μπορούμε επίσης να διαβάσουμε το αρχείο μέσω της `cat`:
Periexomena=$(cat file.txt)
echo "ΑΡΧΗ ΤΟΥ ΑΡΧΕΙΟΥ\n$Periexomena\nΤΕΛΟΣ ΤΟΥ ΑΡΧΕΙΟΥ" # Ο χαρακτήρας "\n"
                                                         # δημιουργεί μια νέα
                                                         # γραμμή
# => ΑΡΧΗ ΤΟΥ ΑΡΧΕΙΟΥ
# => [περιεχόμενα του αρχείου file.txt]
# => ΤΕΛΟΣ ΤΟΥ ΑΡΧΕΙΟΥ

# Μπορούμε να χρησιμοποιήσουμε την εντολή `cp` για να αντιγράψουμε αρχεία ή
# καταλόγους από ένα σημείο σε ένα άλλο.
# Η εντολή `cp` δημιουργεί ΝΕΕΣ εκδοχές των πρωτοτύπων, το οποίο σημαίνει ότι
# μια τροποποίηση του αντιγράφου δεν θα επηρεάσει το πρωτότυπο (και
# αντιστρόφως).
# Να σημειωθεί πως αν υπάρχει ήδη αρχείο ή κατάλογος με το ίδιο όνομα στην ίδια
# θέση με το αντίγραφο, το αντίγραφο θα αντικαταστήσει το αρχείο/κατάλογο και
# άρα τα δεδομένα του θα χαθούν.
cp prototipo.txt antigrafo.txt
cp -r prototipo/ antigrafo/ # Αναδρομική αντιγραφή (αντιγραφή όλων των
                            # περιεχομένων του καταλόγου prototipo/)

# Ενημερωθείτε σχετικά με τις εντολές `scp` και `sftp` αν σχεδιάζετε να
# αντιγράψετε αρχεία από έναν υπολογιστή σε έναν άλλο.
# Η εντολή `scp` μοιάζει πολύ με την `cp`, ενώ η `sftp` είναι πιο διαδραστική.

# Μπορούμε να χρησιμοποιήσουμε την εντολή `mv` για να μετακινήσουμε αρχεία ή
# καταλόγους από μια θέση σε μια άλλη.
# Η εντολή `mv` μοιάζει με την `cp`, με τη διαφορά ότι διαγράφει το πρωτότυπο.
# Η `mv` χρησιμοποιείται επίσης για τη μετονομασία αρχείων!
mv prototipo.txt prototipo2.txt

# Δεδομένου του ότι η Bash δουλεύει στο πλαίσιο του τρέχοντος καταλόγου,
# μπορεί να θελήσουμε να τρέξουμε κάποια εντολή σε κάποιον άλλο κατάλογο.
# Η εντολή `cd` (Change Directory) μας επιτρέπει να αλλάξουμε θέση μέσα στο
# σύστημα αρχείων:
cd ~    # Μετατόπιση στον κατάλογο «home»
cd      # Αυτή η εντολή μας μετατοπίζει επίσης στον κατάλογο «home»
cd ..   # Μετατόπιση προς τα πάνω κατά έναν κατάλογο
        # (για παράδειγμα, μετατόπιση από τη θέση /home/username/Downloads
        # στη θέση /home/username)
cd /home/username/Documents   # Μετατόπιση προς έναν συγκεκριμένο κατάλογο
cd ~/Documents/..    # Μετατόπιση προς τον κατάλογο «home»... σωστά;
cd -    # Μετατόπιση προς τον προηγούμενο κατάλογο
# => /home/username/Documents

# Μπορούμε να χρησιμοποιήσουμε subshells για να δουλέψουμε σε πολλούς
# διαφορετικούς καταλόγους:
(echo "Πρώτα, είμαι εδώ: $PWD") && (cd kapoiosKatalogos; echo "Έπειτα, είμαι εδώ: $PWD")
pwd # Εδώ θα είμαστε στον πρώτο κατάλογο

# Μπορούμε να χρησιμοποιήσουμε την εντολή `mkdir` για να δημιουργήσουμε νέους
# καταλόγους.
mkdir neosKatalogos
# Η επιλογή `-p` επιτρέπει σε ενδιάμεσους καταλόγους να δημιουργηθούν αν
# χρειάζεται.
mkdir -p neosKatalogos/me/epipleon/katalogous
# Αν οι ενδιάμεσοι κατάλογοι δεν υπήρχαν ήδη, η παραπάνω εντολή χωρίς την
# επιλογή `-p` θα είχε επιστρέψει κάποιο λάθος.

# Μπορούμε να διευθύνουμε τις εισόδους και εξόδους των εντολών (χρησιμοποιώντας
# τα κανάλια stdin, stdout και stderr).
# Για παράδειγμα, μπορούμε να «διαβάσουμε» από το stdin μέχρι να βρεθεί ένα
# ^EOF$ (End Of File) και να αντικαταστήσουμε το περιεχόμενο του αρχείου
# hello.py με τις γραμμές που διαβάσαμε έως και πριν το "EOF":
cat > hello.py << EOF
#!/usr/bin/env python
from __future__ import print_function
import sys
print("#stdout", file=sys.stdout)
print("#stderr", file=sys.stderr)
for line in sys.stdin:
    print(line, file=sys.stdout)
EOF

# Μπορούμε να τρέξουμε το πρόγραμμα Python «hello.py» με διάφορες
# ανακατευθύνσεις χρησιμοποιώντας τα stdin, stdout και stderr:
python hello.py < "eisodos.in" # Περνάμε το eisodos.in ως είσοδο στο πρόγραμμα

python hello.py > "eksodos.out" # Ανακατευθύνουμε την έξοδο του προγράμματος
                                # προς το αρχείο eksodos.out

python hello.py 2> "lathos.err" # ανακατευθύνουμε την έξοδο λάθους (stderr)
                                # προς το αρχείο lathos.err

python hello.py > "eksodos-kai-lathos.log" 2>&1
# Ανακατευθύνουμε την κανονική έξοδο (stdout) και την έξοδο λάθους (stderr)
# προς το αρχείο eksodos-kai-lathos.log

python hello.py > /dev/null 2>&1
# Ανακατευθύνουμε όλες τις εξόδους προς τη «μαύρη τρύπα» που λέγεται /dev/null,
# δηλαδή τίποτα δεν θα τυπωθεί στον τερματικό

# Αν θέλετε να προσθέσετε την έξοδο σε κάποιο αρχείο αντί να διαγράψετε τα
# περιεχόμενά του με τη νέα έξοδο, μπορείτε να χρησιμοποιήσετε τον τελεστή
# `>>` αντί στη θέση του `>`:
python hello.py >> "eksodos.out" 2>> "lathos.err"

# Αντικατάσταση του αρχείου eksodos.out, προσθήκη στο αρχείο lathos.err, και
# καταμέτρηση των γραμμών τους:
info bash 'Basic Shell Features' 'Redirections' > eksodos.out 2>> lathos.err
wc -l eksodos.out lathos.err

# Μπορούμε να εκτελέσουμε μια εντολή και να τυπώσουμε τον file descriptor της
# (https://en.wikipedia.org/wiki/File_descriptor)
# Για παράδειγμα: /dev/fd/123
# Δείτε επίσης: man fd
echo <(echo "#καλημέρακόσμε")

# Αντικατάσταση του περιεχομένου του αρχείου eksodos.out με το αλφαριθμητικό
# «#καλημέρακόσμε»:
cat > eksodos.out <(echo "#καλημέρακόσμε")
echo "#καλημέρακόσμε" > eksodos.out
echo "#καλημέρακόσμε" | cat > eksodos.out
echo "#καλημέρακόσμε" | tee eksodos.out >/dev/null

# Εκκαθάριση προσωρινών αρχείων με την επιλογή `-v` (verbose) (προσθέστε την
# επιλογή `-i` για περισσότερη διάδραση)
# ΠΡΟΣΟΧΗ: τα αποτελέσματα της εντολής `rm` είναι μόνιμα.
rm -v eksodos.out lathos.err eksodos-kai-lathos.log
rm -r tempDir/ # Αναδρομική διαγραφή

# Οι εντολές μπορούν να αντικατασταθούν μέσα σε άλλες εντολές χρησιμοποιώντας
# το μοτίβο $( ).
# Το παράδειγμα που ακολουθεί τυπώνει τον αριθμό των αρχείων και των καταλόγων
# στον τρέχων κατάλογο.
echo "Υπάρχουν $(ls | wc -l) αντικείμενα εδώ."

# Μπορούμε να επιτύχουμε το ίδιο αποτέλεσμα με τους χαρακτήρες ``, αλλά δεν
# μπορούμε να τους χρησιμοποιήσουμε αναδρομικά (δηλαδή `` μέσα σε ``).
# Ο προτεινόμενος τρόπος από την Bash είναι το μοτίβο $( ).
echo "Υπάρχουν `ls | wc -l` αντικείμενα εδώ."

# Η Bash έχει επίσης τη δομή `case` που δουλεύει παρόμοια με τη δομή switch
# όπως στην Java ή την C++ για παράδειγμα:
case "$Metavliti" in
    # Λίστα μοτίβων για τις συνθήκες που θέλετε να ορίσετε:
    0) echo "Η μεταβλητή έχει ένα μηδενικό.";;
    1) echo "Η μεταβλητή έχει έναν άσσο.";;
    *) echo "Η μεταβλητή δεν είναι αόριστη (null).";;
esac

# Οι βρόγχοι `for` εκτελούνται τόσες φορές όσο είναι το πλήθος των παραμέτρων
# που τους δίνονται:
# Το περιεχόμενο της μεταβλητής $Metavliti τυπώνεται τρεις φορές.
for Metavliti in {1..3}
do
    echo "$Metavliti"
done
# => 1
# => 2
# => 3

# Μπορούμε επίσης να το γράψουμε πιο «παραδοσιακά»:
for ((a=1; a <= 3; a++))
do
    echo $a
done
# => 1
# => 2
# => 3

# Μπορούμε επίσης να περάσουμε αρχεία ως παραμέτρους.
# Το παράδειγμα που ακολουθεί θα τρέξει την εντολή `cat` με τα αρχεία file1
# και file2:
for Metavliti in file1 file2
do
    cat "$Metavliti"
done

# Μπορούμε ακόμα να χρησιμοποιήσουμε την έξοδο μας εντολής.
# Το παράδειγμα που ακολουθεί θα τρέξει την εντολή `cat` με την έξοδο της
# εντολής `ls`.
for Output in $(ls)
do
    cat "$Output"
done

# Ο βρόγχος `while` έχει ως εξής:
while [ true ]
do
    echo "το «σώμα» του βρόγχου μπαίνει εδώ..."
    break
done
# => το «σώμα» του βρόγχου μπαίνει εδώ...

# Μπορούμε επίσης να ορίσουμε συναρτήσεις, ως εξής:
function synartisi ()
{
    echo "Οι παράμετροι συναρτήσεων δουλεύουν όπως αυτές των προγραμμάτων: $@"
    echo "Και: $1 $2..."
    echo "Αυτή είναι μια συνάρτηση"
    return 0
}
# Ας καλέσουμε την συνάρτηση `synartisi` με δύο παραμέτρους, param1 και param2
synartisi param1 param2
# => Οι παράμετροι συναρτήσεων δουλεύουν όπως αυτές των προγραμμάτων: param1 param2
# => Και: param1 param2...
# => Αυτή είναι μια συνάρτηση

# Ή επίσης:
synartisi2 ()
{
    echo "Ένας άλλος τρόπος να ορίσουμε συναρτήσεις!"
    return 0
}
# Ας καλέσουμε την συνάρτηση `synartisi2` χωρίς παραμέτρους:
synartisi2 # => Ένας άλλος τρόπος να ορίσουμε συναρτήσεις!

# Ας καλέσουμε την πρώτη συνάρτηση:
synartisi "Το όνομά μου είναι" $Onoma

# Υπάρχουν πολλές χρήσιμες εντολές που μπορείτε να μάθετε.
# Για παράδειγμα, αυτή που ακολουθεί τυπώνει τις 10 τελευταίες γραμμές του
# αρχείου file.txt:
tail -n 10 file.txt

# Ενώ αυτή τυπώνει τις 10 πρώτες:
head -n 10 file.txt

# Αυτή ταξινομεί τις γραμμές:
sort file.txt

# Αυτή αναφέρει ή παραλείπει τις γραμμές που επαναλαμβάνονται (η επιλογή
# -d τις αναφέρει):
uniq -d file.txt

# Αυτή τυπώνει μόνο ό,τι βρίσκεται πριν τον πρώτο χαρακτήρα «,» σε κάθε γραμμή:
cut -d ',' -f 1 file.txt

# Αυτή αντικαθιστά κάθε εμφάνιση της λέξης «οκ» με τη λέξη «τέλεια» στο αρχείο
# file.txt (δέχεται επίσης μοτίβα regex):
sed -i 's/οκ/τέλεια/g' file.txt

# Αυτή τυπώνει στο stdout όλες τις γραμμές που είναι συμβατές με κάποιο
# συγκεκριμένο μοτίβο regex.
# Για παράδειγμα, όλες τις γραμμές που ξεκινούν με «καλημέρα» και τελειώνουν με
# «καληνύχτα»:
grep "^καλημέρα.*καληνύχτα$" file.txt

# Η επιλογή `-c` θα τυπώσει τον αριθμό των γραμμών που περιέχουν το μοτίβο:
grep -c "^καλημέρα.*καληνύχτα$" file.txt

# Άλλες χρήσιμες επιλογές:
grep -r "^καλημέρα.*καληνύχτα$" someDir/ # Αναδρομική εκτέλεση μέσα σε κάποιο κατάλογο
grep -n "^καλημέρα.*καληνύχτα$" file.txt # Τυπώνει επίσης τον αριθμό των γραμμών
grep -rI "^καλημέρα.*καληνύχτα$" someDir/ # Αναδρομική εκτέλεση αγνοώντας τα αρχεία binary

# Η ίδια εντολή, αλλά τώρα αγνοώντας τις γραμμές που περιέχουν «αντίο»
grep "^καλημέρα.*καληνύχτα$" file.txt | grep -v "αντίο"

# Αν θέλετε να ψάξετε κυριολεκτικά για ένα αλφαριθμητικό, και όχι για κάποιο
# μοτίβο, μπορείτε να χρησιμοποιήσετε την εντολή `fgrep` (ή `grep -F`):
fgrep "καλημέρα" file.txt

# Η εντολή `trap` επιτρέπει την εκτέλεση μιας εντολής μόλις το πρόγραμμά μας
# λάβει κάποιο σήμα. Στο παράδειγμα που ακολουθεί, η εντολή `trap` θα
# εκτελέσει την εντολή `rm` αν λάβει κάποιο από τα τρία σήματα που ακολουθούν
# (SIGHUP, SIGINT, SIGTERM):
trap "rm $TEMP_FILE; exit" SIGHUP SIGINT SIGTERM

# Η εντολή `sudo` (SuperUser Do) χρησιμοποιείται για να εκτελέσουμε εντολές
# με προνόμια υπερχρήστη (superuser):
ONOMA1=$(whoami)
ONOMA2=$(sudo whoami)
echo "Ήμουν ο $ONOMA1, και έπειτα έγινα ο πιο ισχυρός $ONOMA2"

# Διαβάστε την ενσωματωμένη documentation της Bash χρησιμοποιώντας την εντολή
# `help`:
help
help help
help for
help return
help source
help .

# Διαβάστε τα manpages με την εντολή `man`:
apropos bash
man 1 bash
man bash

# Διαβάστε επίσης την info documentation με την εντολή `info`:
apropos info | grep '^info.*('
man info
info info
info 5 info
info bash
info bash 'Bash Features'
info bash 6
info --apropos bash
```
