


<h1>Ročníkový projekt – Kamerový systém s Raspberry Pi Pico</h1>

<section>
    <h2>Cíl projektu</h2>
    <p>
        Cílem mého ročníkového projektu je sestavení jednoduchého kamerového systému
        pomocí <strong>Raspberry Pi Pico</strong>.
        Hlavní funkcí projektu je automatické přepínání
        do nočního vidění ve chvíli, kdy se setmí.🌜🌟
    </p>
    <p>
        Projekt je zaměřen na praktické využití elektroniky, programování a automatizace.
        Výsledné zařízení by mohlo sloužit například jako základ bezpečnostní kamery
        nebo monitorovacího systému.
    </p>
</section>

<section>
    <h2>Popis funkce projektu</h2>
    <p>
        Raspberry Pi Pico bude propojeno s kamerovým modulem a světelným senzorem.
        Program bude průběžně vyhodnocovat intenzitu okolního světla (pomocí světelného senzoru).
        Až po té době kdy se setmí, tak světelný senroz pošle signál a noční vidění se zapne.
    </p>
    <ul>
      <h2>Zatím zvolené součástky</h2>
        <li>Infračervená LED dioda, 5mm, 940nm čirá: https://rpishop.cz/580649/infracervena-led-dioda-5mm-940nm-cira/</li>
        <li>Metalizovaný rezistor 100 Ω - 0,25 W: https://rpishop.cz/606293/metalizovany-rezistor-100r-0-25-w/</li>
        <li>Modul světelného senzoru - 3 pin: https://rpishop.cz/svetlo/2862-modul-svetelneho-senzoru-3-pin.html/</li>
    </ul>
 
</section>

<section>
    <h2>Současný stav projektu</h2>
    <p>
        V současné době je projekt ve fázi návrhu. 
    </p>
    <ul>
        <li>seznámení se s mikrokontrolérem Raspberry Pi Pico,</li>
        <li>Dizkutace o tom jak to provést</li>
        <li>Hledání vhodných pomůcek</li>
        <li>příprava struktury programu.</li>
    </ul>
    <p>
        Do budoucna bude projekt rozšířen o kompletní zapojení hardwaru, finální verzi
        programu a testování funkčnosti.
    </p>
</section>
<section>
    <h2>Sestavení programu:</h2>
    <p> 
            from machine import ADC, Pin
            import time



            #-----Nastavení pinů-----
            idr = ADC(28)   #pico měří napětí a převádího na čísla, proto čím menší číslo, tím méně tepla
            ir_led = pin(15, pin.OUT) #nastaví pin, ze kterého bude číst hodnoty světla
            #Adc-  umožňuje číst analogovou hodnotu ze senzoru světla
            #Pin- ovládání pinů

            #----- NAstavení prahu-----
            #Čím nižší světlo -> nižší hodnota. Upravit
            #podle skutečnosti:
            THERESHOLD = 25000 #hranice mezi dnem a nocí
            #Hodnota kolem které se přepne den/noc


            while true: #program běží neustále (nekonečná smyčka), dokud to nevypneme pico
                light_value = ldr.read_u16()
                ir_led.value(1)
                print("Hodnota světla:", light_value) # vypíše aktuální hodnotu do konzole
    
            if light_value < THRESYHOLD: #když je tma hoddnota je malá
                 ir_led.value(1)
                 print("NOC: IR LED zapnuto") #vypíše že je noc
    
            else:
                 ir_led.value(0)
                print("DEN: IR LED vypnuto") #vypíše že je den
    
            time.sleep(0.5) #program se na 0,5 sekundy zastaví, aby šetřil výkon a zabránil rychlému přepínání.

    
</section>


<section>
    <h2>Pomocník</h2>
    <p>
        S projektem mi pomáhá Jaroslav Vízner, <strong>Patří mu mé velké díky </strong>
    </p>
   
</section>

<section>
    <h2>Citace a zdroje</h2>
    <ul>
    Při návrhu struktury projektu a formulaci textu byla využita konzultace s jazykovým modelem ChatGPT
    </ul>
</section>

<footer>
    <p>
        Autor projektu: Eliška Kalousová<br>
        Škola: SPŠ Elektrotechniky a informačních technologií, Dobruška<br>
        Školní rok: 2025/2026 <br>
        Třída: T3A <br>
