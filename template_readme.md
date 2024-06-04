Dieses Template dient für die Übungen und Hausaufgaben in Softwareentwicklung 
in c und cpp. 

In Include gehören alle Header-Dateien. 
- Vergiss Guards nicht (ifndef def)
- includiere Header in einander, wenn structs oder anderes benötigt werden
- BEACHTE nicht alle Header in main zu includieren da die Header ineinander sich schon aufrufen

In src gehörn alle .c oder .cpp dateien und die main.
- Ausserhalb der main, werden die Deklarationen aus den headern definiert
- in jede datei werden benötigte Bibliotheken includiert

In Tests gehören alle Test-Dateien.
- Vergiss nicht die Test_fixture, wo die Funktion instanziiert wird als Testfunktion. 
 
