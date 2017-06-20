
EQU	ZUF8R, 0x20		;ein byte

CSEG At 0H
jmp init

;------Interrupt-----
ORG 0Bh
call timer
reti


;-----------MAIN-----------------------------------
init:
	mov tmod, #00000010b  ; T/C0 als 16-Bit-Timer
    	mov IE, #10000010b    ; Timer-Interrupt0 zulassen & Interrupts anschalten
    	mov tl0, #175d
	mov th0, #60d

	MOV P1, #00000001b	;start at begin by using bit 0
	MOV R0, #2fh   ;Speichere die Zahlenreihe oberhalb 30h
	MOV R3, #8d	;Register für Zeile
	MOV R4, #0d	;Register für block
ANF:
;-----------GENERIER EINE ZUFALLSZAHL----------
	call ZUFALL	;Zufallszahl A bestimmen zwischen 00h und ffh
	call zusammen	;Zufallsbit zu Block zusammen ziehen & in R4 schreiben
	setb TCon.4     ; Timer0 starten
	
	;mov P0, ZUF8R	;Zufallsblock an P0 ausgeben
;----------- CASE-ANWEISUNG-------------------------
         mov R2,#00h        ;Zähler initialisieren mit 0
neu:	 add A,#020h        ;die Zufallszahl plus 32
         inc R2            ;Zähler um 1 erhöhen
	 jnc neu           ;falls schon Überlauf, dann weiter - sonst  addiere 32

	 mov A, R2          ;schreib Zahl in A

        jmp ANF


;---------timer-----------------
timer:
	MOV A, P1
	RL A
	MOV P1, A
	DJNZ R3, ZeilenReset
	MOV R3, #8d
	MOV P0, R4
ZeilenReset:
	ret

; ------ Zufallszahlengenerator-----------------
ZUFALL:	
	mov	A, ZUF8R   ; initialisiere A mit ZUF8R
	jnz	ZUB
	cpl	A
	mov	ZUF8R, A
ZUB:	anl	a, #10111000b
	mov	C, P
	mov	A, ZUF8R
	rlc	A
	mov	ZUF8R, A
	ret

;--------Bits zu block zusammen ziehen--------------
ZUSAMMEN:
;-------Blockanfang 7
        jnb 07, P06
        call count
        CJNE R1,#0d, P07_1
        mov R4, #10000000b
        jmp zusammmenEnde
P07_1: 	CJNE R1,#1d, P07_2
    	mov R4, #11000000b
        jmp zusammmenEnde
P07_2:	CJNE R1,#2d, P07_3
    	mov R4, #11100000b
        jmp zusammmenEnde
P07_3:	CJNE R1,#3d, P07_4
    	mov R4, #11110000b
        jmp zusammmenEnde
P07_4:	CJNE R1,#4d, P07_5
    	mov R4, #11111000b
        jmp zusammmenEnde
P07_5:	CJNE R1,#5d, P07_6
    	mov R4, #11111100b
        jmp zusammmenEnde
P07_6:	CJNE R1,#6d, P07_7
    	mov R4, #11111110b
        jmp zusammmenEnde
P07_7:	CJNE R1,#7d,P07_E
    	mov R4, #11111111b
        jmp zusammmenEnde
P07_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 6
P06: jnb 06, P05
        call count
        CJNE R1,#0d, P06_1
        mov R4, #01000000b
        jmp zusammmenEnde
P06_1: 	CJNE R1,#1d, P06_2
    	mov R4, #01100000b
        jmp zusammmenEnde
P06_2:	CJNE R1,#2d, P06_3
    	mov R4, #01110000b
        jmp zusammmenEnde
P06_3:	CJNE R1,#3d, P06_4
    	mov R4, #01111000b
        jmp zusammmenEnde
P06_4:	CJNE R1,#4d, P06_5
    	mov R4, #01111100b
        jmp zusammmenEnde
P06_5:	CJNE R1,#5d, P06_6
    	mov R4, #01111110b
        jmp zusammmenEnde
P06_6:	CJNE R1,#6d, P06_E
    	mov R4, #01111111b
        jmp zusammmenEnde
P06_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 5
P05: jnb 05, P04
        call count
        CJNE R1,#0d, P05_1
        mov R4, #00100000b
        jmp zusammmenEnde
P05_1: 	CJNE R1,#1d, P05_2
    	mov R4, #00110000b
        jmp zusammmenEnde
P05_2:	CJNE R1,#2d, P05_3
    	mov R4, #00111000b
        jmp zusammmenEnde
P05_3:	CJNE R1,#3d, P05_4
    	mov R4, #00111100b
        jmp zusammmenEnde
P05_4:	CJNE R1,#4d, P05_5
    	mov R4, #00111110b
        jmp zusammmenEnde
P05_5:	CJNE R1,#5d, P05_E
    	mov R4, #00111111b
        jmp zusammmenEnde
P05_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 4
P04: jnb 04, P03
        call count
        CJNE R1,#0d, P04_1
        mov R4, #00010000b
        jmp zusammmenEnde
P04_1: 	CJNE R1,#1d, P04_2
    	mov R4, #00011000b
        jmp zusammmenEnde
P04_2:	CJNE R1,#2d, P04_3
    	mov R4, #00011100b
        jmp zusammmenEnde
P04_3:	CJNE R1,#3d, P04_4
    	mov R4, #00011110b
        jmp zusammmenEnde
P04_4:	CJNE R1,#4d, P04_E
    	mov R4, #00011111b
        jmp zusammmenEnde
P04_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 3
P03: jnb 03, P02
        call count
        CJNE R1,#0d, P03_1
        mov R4, #00001000b
        jmp zusammmenEnde
P03_1: 	CJNE R1,#1d, P03_2
    	mov R4, #00001100b
        jmp zusammmenEnde
P03_2:	CJNE R1,#2d, P03_3
    	mov R4, #00001110b
        jmp zusammmenEnde
P03_3:	CJNE R1,#3d, P03_E
    	mov R4, #00001111b
        jmp zusammmenEnde
P03_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten
        
;-------Blockanfang 2
P02: jnb 02, P01
        call count
        CJNE R1,#0d, P02_1
        mov R4, #00000100b
        jmp zusammmenEnde
P02_1: 	CJNE R1,#1d, P02_2
    	mov R4, #00000110b
        jmp zusammmenEnde
P02_2:	CJNE R1,#2d, P02_E
    	mov R4, #00000111b
        jmp zusammmenEnde
P02_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 1
P01: jnb 01, P00
        call count
        CJNE R1,#0d, P01_1
        mov R4, #00000010b
        jmp zusammmenEnde
P01_1: 	CJNE R1,#1d, P01_E
    	mov R4, #00000011b
        jmp zusammmenEnde
P01_E:	jmp zusammmenEnde	;dieser Fall darf nicht eintreten

;-------Blockanfang 0
P00: jnb 00, zusammmenEnde
zusammmenEnde:
        ret

;------zaehlt restliche felder---------
count:
	mov R1,#00h        ;Zähler initialisieren mit 0 
	
     	jnb 07, B06
        inc R1
B06: 	jnb 06, B05
        inc R1
B05: 	jnb 05, B04
        inc R1
B04: 	jnb 04, B03
        inc R1
B03: 	jnb 03, B02
        inc R1
B02: 	jnb 02, B01
        inc R1
B01: 	jnb 01, B00
        inc R1
B00: 	jnb 00, alleGezaelt
        inc R1
alleGezaelt:
	dec R1
        ret

end
