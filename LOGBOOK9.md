## Secret Key Encryption Lab

#### Task 1


After analysing the frequency analysis, by running the command ```./freq.py``` we began to substitute diferent characters in order to find the ecrypted message. The final command was:

```$  tr ’ytnvupxmqiehsbzdaclrgfjk’ ’THEANDOISLPRKFUYCMWGBVQX’ < ciphertext.txt > substituted.txt```

By running it, we discovered the message:

```
THE OSCARS TURN  ON SUNDAY WHICH SEEMS ABOUT RIGHT AFTER THIS LONG STRANGE
AWARDS TRIP THE BAGGER FEELS LIKE A NONAGENARIAN TOO

THE AWARDS RACE WAS BOOKENDED BY THE DEMISE OF HARVEY WEINSTEIN AT ITS OUTSET
AND THE APPARENT IMPLOSION OF HIS FILM COMPANY AT THE END AND IT WAS SHAPED BY
THE EMERGENCE OF METOO TIMES UP BLACKGOWN POLITICS ARMCANDY ACTIVISM AND
A NATIONAL CONVERSATION AS BRIEF AND MAD AS A FEVER DREAM ABOUT WHETHER THERE
OUGHT TO BE A PRESIDENT WINFREY THE SEASON DIDNT oUST SEEM EXTRA LONG IT WAS
EXTRA LONG BECAUSE THE OSCARS WERE MOVED TO THE FIRST WEEKEND IN MARCH TO
AVOID CONFLICTING WITH THE CLOSING CEREMONY OF THE WINTER OLYMPICS THANKS
PYEONGCHANG

ONE BIG QUESTION SURROUNDING THIS YEARS ACADEMY AWARDS IS HOW OR IF THE
CEREMONY WILL ADDRESS METOO ESPECIALLY AFTER THE GOLDEN GLOBES WHICH BECAME
A oUBILANT COMINGOUT PARTY FOR TIMES UP THE MOVEMENT SPEARHEADED BY 
POWERFUL HOLLYWOOD WOMEN WHO HELPED RAISE MILLIONS OF DOLLARS TO FIGHT SEXUAL
HARASSMENT AROUND THE COUNTRY

SIGNALING THEIR SUPPORT GOLDEN GLOBES ATTENDEES SWATHED THEMSELVES IN BLACK
SPORTED LAPEL PINS AND SOUNDED OFF ABOUT SEXIST POWER IMBALANCES FROM THE RED
CARPET AND THE STAGE ON THE AIR E WAS CALLED OUT ABOUT PAY INEQUITY AFTER
ITS FORMER ANCHOR CATT SADLER QUIT ONCE SHE LEARNED THAT SHE WAS MAKING FAR
LESS THAN A MALE COHOST AND DURING THE CEREMONY NATALIE PORTMAN TOOK A BLUNT
AND SATISFYING DIG AT THE ALLMALE ROSTER OF NOMINATED DIRECTORS HOW COULD
THAT BE TOPPED

AS IT TURNS OUT AT LEAST IN TERMS OF THE OSCARS IT PROBABLY WONT BE

WOMEN INVOLVED IN TIMES UP SAID THAT ALTHOUGH THE GLOBES SIGNIFIED THE
INITIATIVES LAUNCH THEY NEVER INTENDED IT TO BE oUST AN AWARDS SEASON
CAMPAIGN OR ONE THAT BECAME ASSOCIATED ONLY WITH REDCARPET ACTIONS INSTEAD
A SPOKESWOMAN SAID THE GROUP IS WORKING BEHIND CLOSED DOORS AND HAS SINCE
AMASSED  MILLION FOR ITS LEGAL DEFENSE FUND WHICH AFTER THE GLOBES WAS
FLOODED WITH THOUSANDS OF DONATIONS OF  OR LESS FROM PEOPLE IN SOME 
COUNTRIES


NO CALL TO WEAR BLACK GOWNS WENT OUT IN ADVANCE OF THE OSCARS THOUGH THE
MOVEMENT WILL ALMOST CERTAINLY BE REFERENCED BEFORE AND DURING THE CEREMONY 
ESPECIALLY SINCE VOCAL METOO SUPPORTERS LIKE ASHLEY oUDD LAURA DERN AND
NICOLE KIDMAN ARE SCHEDULED PRESENTERS

ANOTHER FEATURE OF THIS SEASON NO ONE REALLY KNOWS WHO IS GOING TO WIN BEST
PICTURE ARGUABLY THIS HAPPENS A LOT OF THE TIME INARGUABLY THE NAILBITER
NARRATIVE ONLY SERVES THE AWARDS HYPE MACHINE BUT OFTEN THE PEOPLE FORECASTING
THE RACE SOCALLED OSCAROLOGISTS CAN MAKE ONLY EDUCATED GUESSES

THE WAY THE ACADEMY TABULATES THE BIG WINNER DOESNT HELP IN EVERY OTHER
CATEGORY THE NOMINEE WITH THE MOST VOTES WINS BUT IN THE BEST PICTURE
CATEGORY VOTERS ARE ASKED TO LIST THEIR TOP MOVIES IN PREFERENTIAL ORDER IF A
MOVIE GETS MORE THAN  PERCENT OF THE FIRSTPLACE VOTES IT WINS WHEN NO
MOVIE MANAGES THAT THE ONE WITH THE FEWEST FIRSTPLACE VOTES IS ELIMINATED AND
ITS VOTES ARE REDISTRIBUTED TO THE MOVIES THAT GARNERED THE ELIMINATED BALLOTS
SECONDPLACE VOTES AND THIS CONTINUES UNTIL A WINNER EMERGES

IT IS ALL TERRIBLY CONFUSING BUT APPARENTLY THE CONSENSUS FAVORITE COMES OUT
AHEAD IN THE END THIS MEANS THAT ENDOFSEASON AWARDS CHATTER INVARIABLY
INVOLVES TORTURED SPECULATION ABOUT WHICH FILM WOULD MOST LIKELY BE VOTERS
SECOND OR THIRD FAVORITE AND THEN EQUALLY TORTURED CONCLUSIONS ABOUT WHICH
FILM MIGHT PREVAIL

IN  IT WAS A TOSSUP BETWEEN BOYHOOD AND THE EVENTUAL WINNER BIRDMAN
IN  WITH LOTS OF EXPERTS BETTING ON THE REVENANT OR THE BIG SHORT THE
PRIwE WENT TO SPOTLIGHT LAST YEAR NEARLY ALL THE FORECASTERS DECLARED LA
LA LAND THE PRESUMPTIVE WINNER AND FOR TWO AND A HALF MINUTES THEY WERE
CORRECT BEFORE AN ENVELOPE SNAFU WAS REVEALED AND THE RIGHTFUL WINNER
MOONLIGHT WAS CROWNED

THIS YEAR AWARDS WATCHERS ARE UNEQUALLY DIVIDED BETWEEN THREE BILLBOARDS
OUTSIDE EBBING MISSOURI THE FAVORITE AND THE SHAPE OF WATER WHICH IS
THE BAGGERS PREDICTION WITH A FEW FORECASTING A HAIL MARY WIN FOR GET OUT

BUT ALL OF THOSE FILMS HAVE HISTORICAL OSCARVOTING PATTERNS AGAINST THEM THE
SHAPE OF WATER HAS  NOMINATIONS MORE THAN ANY OTHER FILM AND WAS ALSO
NAMED THE YEARS BEST BY THE PRODUCERS AND DIRECTORS GUILDS YET IT WAS NOT
NOMINATED FOR A SCREEN ACTORS GUILD AWARD FOR BEST ENSEMBLE AND NO FILM HAS
WON BEST PICTURE WITHOUT PREVIOUSLY LANDING AT LEAST THE ACTORS NOMINATION
SINCE BRAVEHEART IN  THIS YEAR THE BEST ENSEMBLE SAG ENDED UP GOING TO
THREE BILLBOARDS WHICH IS SIGNIFICANT BECAUSE ACTORS MAKE UP THE ACADEMYS
LARGEST BRANCH THAT FILM WHILE DIVISIVE ALSO WON THE BEST DRAMA GOLDEN GLOBE
AND THE BAFTA BUT ITS FILMMAKER MARTIN MCDONAGH WAS NOT NOMINATED FOR BEST
DIRECTOR AND APART FROM ARGO MOVIES THAT LAND BEST PICTURE WITHOUT ALSO
EARNING BEST DIRECTOR NOMINATIONS ARE FEW AND FAR BETWEEN
```




#### Task 2

In this task, we created a file: ```plaintext.txt``` and we encrypted and decrypted it using three different AES modes: AES-128-ECB, AES-128-CBC, and AES-128-CTR.

 ##### 1. Encrypting the File
 ###### AES-128-ECB
 
 We used the command:

 ```openssl enc -aes-128-ecb -e -in plaintext.txt -out cipher_ecb.bin -K 00112233445566778889aabbccddeeff ```

- ```-aes-128-ecb``` : Specifies the cipher mode as ECB.
- ```-e``` : Indicates encryption.
- ```-in plaintext.txt``` : The input file to be encrypted.
- ```-out cipher_ecb.bin``` : The output encrypted file.
- ```-K``` : Provides the encryption key in hexadecimal format. A 128-bit key is required for AES-128.

###### AES-128-CBC

 We used the command:
 
 ```openssl enc -aes-128-cbc -e -in plaintext.txt -out cipher_cbc.bin -K 00112233445566778889aabbccddeeff -iv 0102030405060708```
 - Same as ECB mode, but with an additional ```-iv``` parameter to specify the initialization vector (IV). The IV introduces randomness to ensure identical plaintext blocks result in different ciphertext blocks.

###### AES-128-CTR

We used the command:

```openssl enc -aes-128-ctr -e -in plaintext.txt -out cipher_ctr.bin -K 00112233445566778889aabbccddeeff -iv 0102030405060708```
- Similar to CBC mode, CTR also requires an IV. In CTR, the IV serves as a nonce and is incremented for each block to generate a unique counter.

##### 2. Decrypting the File

 
###### AES-128-ECB
 
 We used the command:

 ```openssl enc -aes-128-ecb -d -in cipher_ecb.bin -out decrypted_ecb.txt -K 00112233445566778889aabbccddeeff```

- ```-d``` : Specifies decryption.
- The rest of the parameters remain the same as in the encryption step.128-bit key is required for AES-128.

###### AES-128-CBC

 We used the command:
 
 ```openssl enc -aes-128-cbc -d -in cipher_cbc.bin -out decrypted_cbc.txt -K 00112233445566778889aabbccddeeff -iv 0102030405060708```
 - The IV, ```-iv```, is necessary for decryption to correctly reverse the chaining process used in encryption.

###### AES-128-CTR

We used the command:

```openssl enc -aes-128-ctr -d -in cipher_ctr.bin -out decrypted_ctr.txt -K 00112233445566778889aabbccddeeff -iv 0102030405060708```
- The same IV used for encryption is required for decryption to ensure correct counter synchronization.

 ##### "When encrypting, which flags did you need to specify? What is the difference between these different modes?"
###### Flags Required for Encryption:

- ```-K``` : Specifies the encryption key in hexadecimal format (32 characters for AES-128).
- ```-e``` : Indicates encryption.
- ```-in``` : Specifies the input plaintext file to encrypt.
- ```-out``` : Specifies the output file to store the ciphertext.
- ```-iv``` (for CBC and CTR): Specifies the initialization vector (IV) in hexadecimal format (16 characters).

###### Differences Between Modes:

- AES-128-ECB:

Encrypts blocks independently.
Does not require an IV, making it simpler but vulnerable to pattern detection.
- AES-128-CBC:

Uses an IV to chain encryption across blocks, eliminating plaintext patterns.
Requires synchronization of the IV for both encryption and decryption.

- AES-128-CTR:

Converts the block cipher into a stream cipher by combining a counter (derived from IV) with the plaintext.
Allows random access to encrypted data and supports parallel processing.


 ##### "When decrypting, which flags did you need to specify? What is the main difference between AES-128-CTR and the other modes?"

###### Flags Required for Decryption:

- ```-K``` : Specifies the decryption key in hexadecimal format.
- ```-d``` : Indicates decryption.
- ```-in``` : Specifies the input ciphertext file.
- ```-out``` : Specifies the output file to store the decrypted plaintext.
- ```-iv``` (for CBC and CTR): The same IV used for encryption must be provided to reverse the process correctly.

###### Main Difference Between AES-128-CTR and the Other Modes:

- Error Handling:

In CTR mode, decryption errors caused by corrupted ciphertext affect only the corresponding block (byte-level independence). This is because CTR does not use chaining between blocks.
In CBC mode, a single corrupted block causes errors in that block and all subsequent blocks, as decryption relies on the chaining process.

- Parallel Processing:

CTR allows independent decryption of blocks, supporting parallelism.
ECB and CBC require sequential processing.
#### Task 5