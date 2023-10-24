# text-analyzer

Aceasta este o aplicație menită să analizeze care sunt frecvențele cuvintelor din text, frecvența unor cuvinte cu o anumita lungime, etc.
In acest scop, în implementare am construit o tabela hash in care sa păstrez cuvintele întâlnite, cu mențiunea că se vor considera cuvinte șirurile de caractere (de lungime >= 3) formate din litere mici/mari, ’-’.

În cadrul acestui program au fost implementate următoarele comenzi:
- _insert text_ (pentru inserarea cuvintelor în tabela hash)
- _print_ (afișarea conținutului tabelei)
- _print c n_, unde c reprezintă prima litera a cuvintelor, iar n lungimea acestora (afișarea cuvintelor care încep cu o anumită literă și au o anumită lungime)
- _print n_ (afișare cuvinte care apar de maxim n ori)

  ## Implementare

  Am citit datele efective din fisier (dat ca argument main-ului) folosind getline,
si le-am parsat folosind strtok_r (pt thread safety). Initializez o tabela hash.
Pentru a introduce cuvintele in tabela hash, mai intai verific daca sunt destul
de lungi (mai mari de 2 caractere) si daca sunt cuvinte (am verificat ca primul
caracter din cuvant este o litera).
Daca s-a introdus un cuvant valid, atunci imi construiesc o structura (TCuvant *) care
sa retina cuvantul in sine (char *) si frecventa lui (am initializat-o cu 1). Apeland
functia de inserare (ins_in_hash), exista trei cazuri principale:

- daca exista deja o lista in tabela hash care sa retina cuvintele care incep cu
prima litera a cuvantului (searchlist returneaza un pointer), trebuie sa caut in lista respectiva o sublista de cuvinte
de aceeasi lungime ca cel de inserat. Daca exista, il introduc in sublista, avand grija
sa nu introduc duplicate (cresc frecventa cuvantului din tabela hash in cazul in care el
deja exista in sublista) folosind functia ins_in_subList;

- daca nu exista sublista corespunzatoare cuvantului in tabela hash (searchlist returneaza
NULL), trebuie sa construiesc o celula in care sa retin date despre sublista (TSublist
retine lungimea  cuvintelor din ea si o lista cu acele cuvinte), sa introduc cuvantul in
sublista noua, avand grija ca aceasta sa nu strice ordinea alfabetica a sublistelor
(am folosit functia searchdesc), si sa adaug sublista in tabela hash;

- daca nu gasesc o sublista dupa care sa introduc sublista noua (loc == NULL, loc fiind
pointerul la sublista inaintea caruia introduceam sublista noua, sau a->v + code e pur si
simplu goala), atunci o inserez la inceputul listei a->v + code.

Pentru afisari (adica print, prin a 1, prin 5), am incercat sa verific daca primul argument
dat lui print este o litera sau o crifa:

- daca mi se da o crifa ca prim argument, atunci trebuie sa caut in intreaga tabela hash cuvinte
care au frecventa mai mica sau egala cu argumentul dat folosind functia search_hash.

- daca este o litera, sigur exista inca un parametru care sa descrie lungimea cuvintelor.
Am folosit functia show_given_subl care sa afizese toate elementele din sublista care contine
cuvinte care sa inceapa cu litera data si care sa aiba lungimea data ca al doilea argument.
