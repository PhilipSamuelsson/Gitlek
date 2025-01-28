
# En fin jävla header 

*En projektbeskrivning som är kursiv.*



[link](https://www.example.com/my%20great%20page)

---

> ETT BLOCKCITAT! 

Nedan följer en ordnad lista i Markdown-format över hur du installerar och får en lampa (LED) att blinka med en Raspberry Pi Pico.

    Förberedelser
        Material: Raspberry Pi Pico, en LED, ett motstånd (t.ex. 220 Ω), kopplingskablar och en USB-kabel.
        Programvara: Thonny (eller annan kompatibel IDE) och MicroPython-firmware för Raspberry Pi Pico.

    Ladda ner MicroPython-firmware
        Gå till Raspberry Pis officiella webbplats eller MicroPython.org för att hämta den senaste .uf2-filen för Raspberry Pi Pico.

    Sätt Picon i bootloader-läge
        Håll in BOOTSEL-knappen på Raspberry Pi Pico.
        Anslut Picon till din dator via USB medan du fortfarande håller in knappen.
        Släpp BOOTSEL-knappen när Picon dyker upp som en extern lagringsenhet i ditt filsystem.

    Ladda MicroPython på Picon
        Dra och släpp den nedladdade .uf2-filen till din Pico-enhet i filhanteraren (datorn behandlar då Picon som ett USB-minne).
        När överföringen är klar startar Picon om och är redo att köras med MicroPython.

    Installera och starta Thonny
        Ladda ner och installera Thonny från thonny.org.
        Öppna Thonny och välj sedan Run → Select Interpreter (eller motsvarande inställning i din version av Thonny).
        Under “Which interpreter or device” väljer du MicroPython (Raspberry Pi Pico) och bekräftar.

    Koppla in LED och motstånd
        Anslut kortbenet (katoden) på LED:en till GND på Picon.
        Anslut långbenet (anoden) via motståndet till en valfri GPIO-pin, till exempel GPIO 15.
        Se till att du har rätt värde på motståndet (220 Ω är vanligt) för att skydda LED:en och Picon.

    Skriv ett enkelt blink-program i Thonny
    Öppna ett nytt skript i Thonny och klistra in följande kodexempel (anpassa pin-numret om du använt ett annat GPIO-nummer):
	
	    Kör och testa programmet
        Spara filen som exempelvis blink.py (eller direkt som main.py för att det ska starta automatiskt vid ström på Picon).
        Klicka på Run i Thonny för att ladda upp koden till Picon.
        Din LED bör nu blinka med 1 sekund intervall.

    (Valfritt) Spara som main.py för automatisk start
        Om du vill att blinkprogrammet ska starta automatiskt när Picon spänningssätts, kan du spara det som main.py direkt på Picon.
        Koppla sedan från och anslut Picon igen för att bekräfta att programmet körs automatiskt.

    Felsökning
        Ingen USB-enhet hittas: Se till att du håller BOOTSEL intryckt innan du ansluter Picon.
        LED blinkar ej: Verifiera att du anslutit LED och motstånd rätt (rätt polaritet och GPIO-pin).
        Felaktigt GPIO-nummer: Säkerställ att koden använder rätt pin där LED är ansluten.

När du följt dessa steg bör du ha en fungerande blinkande LED på din Raspberry Pi Pico!
