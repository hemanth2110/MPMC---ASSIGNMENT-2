EXPERIMENT: Timer-based LED Toggle using 8051

Write an assembly language program in 8051 to generate a 5 ms delay using Timer 1 in Mode 1 and toggle an LED connected to Port 1.7 continuously.


AIM:
To write an assembly language program in 8051 microcontroller to generate a 5 ms delay using Timer 1 in Mode 1 and continuously toggle an LED connected to Port 1.7

ALGORITHM:

Start the program at address 0000H.
Select Timer 1, Mode 1 (16-bit Timer) by loading TMOD with 10H.
Load Timer 1 registers with initial values for a 5 ms delay.
For 12 MHz crystal, machine cycle = 1 µs
Required count = 65536 − 5000 = EC78H
→ TH1 = ECH, TL1 = 78H
Start the timer using SETB TR1.
Wait until TF1 = 1 (timer overflow → 5 ms delay complete).
Stop the timer and clear TF1 for next delay cycle.
Toggle P1.7 using CPL P1.7.

PROGRAM:
```
ORG 0000H        

MAIN:
    MOV TMOD, #10H    ; Timer 1 in Mode 1 (16-bit timer)
    CLR P1.7          ; Initialize LED OFF

REPEAT:
    CPL P1.7          ; Toggle LED connected to Port 1.7
    ACALL DELAY       ; Call 5 ms delay subroutine
    SJMP REPEAT       ; Repeat forever

;------------------------------------
; Subroutine: 5 ms delay using Timer 1
;------------------------------------
DELAY:
    MOV TH1, #0ECH    ; Load high byte for 5 ms delay
    MOV TL1, #078H    ; Load low byte for 5 ms delay
    SETB TR1          ; Start Timer 1

WAIT:
    JNB TF1, WAIT     ; Wait until Timer 1 overflows
    CLR TR1           ; Stop Timer 1
    CLR TF1           ; Clear overflow flag
    RET               ; Return to main program

END

```

OUTPUT:
<img width="1919" height="1021" alt="Screenshot 2025-10-27 182450" src="https://github.com/user-attachments/assets/7b1ba353-c2c6-46e2-9649-04adbb00805a" />
<img width="1919" height="1019" alt="Screenshot 2025-10-27 182410" src="https://github.com/user-attachments/assets/d80ed266-40f4-4600-a351-7953cae91a7b" />

RESULT:
Thus, the assembly language program for generating a 5 ms delay using Timer 1 in Mode 1 and toggling an LED connected to Port 1.7 was successfully executed and verified in Keil µVision.
