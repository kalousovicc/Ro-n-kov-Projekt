
<h1>Ročníkový projekt – Kamerový systém s Raspberry Pi Pico</h1>

<section>
    <h2>Cíl projektu</h2>
    <p>
        Cílem mého ročníkového projektu je sestavení jednoduchého kamerového systému
        pomocí <strong>mikrokontroléru</strong>.
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
      <h2>Součástky</h2>
        <li>Infračervená LED dioda, 5mm, 940nm čirá: https://rpishop.cz/580649/infracervena-led-dioda-5mm-940nm-cira/</li>
        <li>Metalizovaný rezistor 100 Ω - 0,25 W: https://rpishop.cz/606293/metalizovany-rezistor-100r-0-25-w/</li>
        <li>Modul světelného senzoru - 3 pin: https://rpishop.cz/svetlo/2862-modul-svetelneho-senzoru-3-pin.html/</li>
        Breadborad (bude to jen pro projekct takže to stačí)   
    </ul>
 
</section>
<section> 
<h2> Popis Funkce kamery a infračervených ledek</h2>

<p> Led diody svítí infračerveným světlem, které lidské oko nevidí, ale senzor ho vidí moc dobře, když ho kamera zachití obraz vypadá jako noční vidění.NA co si dávat pozor? Na to že berou velká proud a nesmí se napájet přímo z mikrokontroléru, protože by mohli shořet, proto k tomu budu muset použít transiztor </p>

</section>

<section>
    <h2>Záměr projektu</h2>
    <ul>
        <li>seznámení se s mikrokontrolérem </li>
        <li>zjištění o funkčnosti infračervených ledek</li>
        <li>Sepsat kod pro funkčnost</li>
        <li>vyzkoušet pracovat s breadboardem a součástami</li>
    </ul>
</section>
<section>
    <h2>Sestavení programu:</h2>
</section>

```py
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


while true: #program běží neustále (nekonečná smyčka), dokud nevypneme pico
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
```
<section>
    <h2>Dokumentace o postupu</h2>
    Projekt jsem měla vymyšlení v hlavě, mikrokontrolér bude detekovat zda je den či noc a jakmile zjistí že je noc tak na kameře zapne noční vidění, ale když jsem koukala na kamery s nočním viděním tak buď nebyly kompatibilní a nebo byly drahé, takže jsem vymyslela že použiju infračervené diody sice to nebude tak učínné, ale zase to bude více zajímavé v ohledu studija. Jak to vlastně bude fungovat? Je to jednoduché infračervedné diody místo viditelného světla vyzařují infračervené záření, což lidké oko nevidí, ale kamrey ano, protože jsou velmi citlivé na infračervené vlny, infračervené diody svítí infra světlem, které my nevidíme, ale kamera an, proto jsou vhodné na použítí nočního vidění pro kamery. Udělala jsem kod tak že ten senzor bude stále detekovat a zasílat data do mikrokontroléru, sice se to bude opakovat furt a mohla bych to udělat jinak aby to furt se to furt neptalo zda je den či noc, ale je to jen pro pojekt takže to
moc nevadí, ale třeba někdy v budoucnu to udělam znova a lépe, za zapojení jsem použila breadbord, protože jsem si častky půjčovala tak abyc to vratila v pořádku, 
se spojováním mi pomahal Jaroslav Vízner a dali jsme to do kupy, v přidaných souv´borech jsem vám přidala fotku z kamery jak to vypadalo v úplné tmě (je to foceno u mně za barákem.
    
</section>
<section>
    <h2>Pomocník</h2>
    <p>
        S projektem mi pomáhá Jaroslav Vízner, <strong>Patří mu mé velké díky. Jakub Daško mi pujčil součástky, takže mu taky prevelice děkuji </strong>
    </p>
   
</section>

<section>
    <h2>Citace a zdroje</h2>
    <ul>
    WILLIAMS, Barrett a CHATGPT. Raspberry Pi Security: Build Your Own DIY Home Security System with Pi. Barrett Williams, 2025.
    </ul>
</section>

<footer>
    <p>
        Autor projektu: Eliška Kalousová<br>
        Škola: SPŠ Elektrotechniky a informačních technologií, Dobruška<br>
        Školní rok: 2025/2026 <br>
        Třída: T3A <br>
    </p>
