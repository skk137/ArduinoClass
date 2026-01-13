# ArduinoClass  
## Κώδικας Εργαστηρίου 1

### Αυτόματο σύστημα φωτισμού με LDR και LED

**Συνδεσμολογία:**
- LDR → A0  
- LED → D9  

Το σύστημα ανάβει το LED όταν το επίπεδο φωτισμού είναι χαμηλό (σκοτάδι) και το σβήνει όταν υπάρχει αρκετό φως.

---

## Κώδικας Arduino

```cpp
// Αυτόματο σύστημα φωτισμού με LDR και LED
// LDR -> A0, LED -> D9

const int LDR_PIN = A0;
const int LED_PIN = 9;

// Τιμή κατωφλίου (threshold)
// Ανάλογα με τη συνδεσμολογία και τον φωτισμό
int threshold = 400;

void setup() {
  pinMode(LED_PIN, OUTPUT);

  // 9600 bits/δευτερόλεπτο : αποτελεί προεπιλεγμένη και ασφαλής τιμή
  Serial.begin(9600); // Εμφάνιση τιμών στο Serial Monitor
}

void loop() {
  int lightValue = analogRead(LDR_PIN); // Εύρος τιμών: 0–1023

  // Εκτύπωση τιμής για πειραματισμό και ρύθμιση threshold
  Serial.println(lightValue);

  //Όταν υπάρχει σκοτάδι (τιμή < threshold) ανάβει το LED
  if (lightValue < threshold) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }

  // Μικρή καθυστέρηση για σταθερότητα και αποφυγή τρεμοπαίγματος
  delay(200);

}

