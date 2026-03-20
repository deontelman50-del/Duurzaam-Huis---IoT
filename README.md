# Duurzaam-Huis---IoT

// NodeMCU pinnen voor lampen
// D3 = GPIO0, D5 = GPIO14, D6 = GPIO12

int A, B, C, D;

void setup() {
  pinMode(D3, OUTPUT);
  pinMode(D5, OUTPUT);
  pinMode(D6, OUTPUT);

  Serial.begin(115200);

  // Random seed
  randomSeed(analogRead(A0));
}

void loop() {
  // Genereer continu nieuwe willekeurige getallen
  A = random(999);
  B = random(999);
  C = random(999);
  D = random(999);

  Serial.print("A = "); Serial.print(A);
  Serial.print(" | B = "); Serial.print(B);
  Serial.print(" | C = "); Serial.print(C);
  Serial.print(" | D = "); Serial.println(D);

  // Lamp D3 aan/uit
  if (A > B || A < C) {
    digitalWrite(D3, HIGH);
  } else {
    digitalWrite(D3, LOW);
  }

  // Lamp D5 aan/uit
  if (C > A && A < B) {
    digitalWrite(D5, HIGH);
  } else {
    digitalWrite(D5, LOW);
  }

  // Lamp D6 aan/uit
  if (B > C && B > A && C < A) {
    digitalWrite(D6, HIGH);
  } else {
    digitalWrite(D6, LOW);
  }

  // Snel knipperen als D het grootste getal is
  if (D > A && D > B && D > C) {
    for (int i = 0; i < 5; i++) { // knipper 5x snel
      digitalWrite(D3, HIGH);
      digitalWrite(D5, HIGH);
      digitalWrite(D6, HIGH);
      delay(100);
      digitalWrite(D3, LOW);
      digitalWrite(D5, LOW);
      digitalWrite(D6, LOW);
      delay(100);
    }
  }

  delay(500); // korte pauze voordat nieuwe getallen worden gegenereerd
}
