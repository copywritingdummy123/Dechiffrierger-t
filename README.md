# Dechiffriergerät-t
Ein Konsolenprogramm zur Ver- und Entschlüsselung von Nachrichten. 2 Nutzer können mit diesem Programm verschlüsselte Nachrichten senden oder empfangen. Es ersetzt ein manuelles Dechiffriergerät.

using System;

class Program
{
    static void Main()
    {
        while (true)
        {
            Console.WriteLine("Dechiffriergerät");
         
            Console.WriteLine("1 Verschlüsseln");
            Console.WriteLine("2 Entschlüsseln");
            Console.WriteLine("3 Wie funktioniert das hier?");
            Console.WriteLine("4 Beenden");
            Console.Write("Auswahl: ");

            string eingabe = Console.ReadLine();

            if (eingabe == "1") //Verschlüsseln
            {
                Console.Write("Gib deine Nachricht ein: ");
                string nachricht = Console.ReadLine();

                Console.Write("Schlüssel (Zahl) eingeben: ");
                int schluessel = int.Parse(Console.ReadLine());

                string ergebnis = Verschluesseln(nachricht, schluessel);
                Console.WriteLine("Verschlüsselte Nachricht: " + ergebnis);
            } //Verschlüsseln
            else if (eingabe == "2") //Entschlüsseln
            {
                Console.Write("Gib deine Nachricht ein: ");
                string nachricht = Console.ReadLine();

                Console.Write("Schlüssel (Zahl) eingeben: ");
                int schluessel = int.Parse(Console.ReadLine());

                string ergebnis = Entschluesseln(nachricht, schluessel);
                Console.WriteLine("Entschlüsselter Text: " + ergebnis);
            }//Entschlüsseln
            else if (eingabe == "4")//
            {
                Console.WriteLine("Programm beendet.");
                break;
            }//beenden

            else if (eingabe == "3")// Erklärung
            {
                Console.WriteLine("");
                Console.WriteLine("2 Nutzer, die beide dieses Programm installiert haben, können Nachrichten, die sie schicken möchten, ver oder entschlüsseln.");
                Console.WriteLine("Die Buchstaben der Nachricht werden im Alphabet um eine bestimmte Anzahl verschoben. Diese Anzahl ist der Schlüssel.");
                Console.WriteLine("Wenn beide Nutzer denselben Schlüssel eingeben, können nur Sender und Empfänger die eigentliche Nachricht verstehen.");
                Console.WriteLine("Dechiffrierungen auf derselben Grundlage (nur komplexer) wurden in beiden Weltkriegen verwenden und haben den Verlauf der Geschichte beeinflusst.");
                break;
            }

            else
            {
                Console.WriteLine("Ungültige Eingabe.");
            }
        }
    }

    static string Verschluesseln(string nachricht, int schluessel)
    {
        string ergebnis = "";

        foreach (char buchstabe in nachricht)
        {
            if (char.IsLetter(buchstabe))
            {
                char start = char.IsUpper(buchstabe) ? 'A' : 'a';
                int verschoben = (buchstabe - start + schluessel) % 26;

                if (verschoben < 0)
                    verschoben += 26;

                ergebnis += (char)(start + verschoben);
            }
            else
            {
                ergebnis += buchstabe;
            }
        }

        return ergebnis;
    }

    static string Entschluesseln(string nachricht, int schluessel)
    {
        return Verschluesseln(nachricht, -schluessel);
    }
}
