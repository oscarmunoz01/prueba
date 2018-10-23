%include    "io.mac"
BUF_SIZE    EQU  4


.Data
msg1    db    "***********************Bienvenido a la CPU*********************",0
msg2    db    "Menu de opciones:",0
msg3     db    "1. Ver Registros",0
msg4    db    "2. Ver memoria",0
msg5     db    "3. Correr programa",0
msg6    db    "4. Salir",0

.Udata
resp      resb 4
buffe     resb    BUF_SIZE
R1      resb 4
R2      resb  4
R3      resb  4
R4      resb  4
PC      resb  8
IR      resb  8



.CODE

.STARTUP

PutStr msg1
nwln
PutStr msg2
nwln
PutStr msg3
nwln
PutStr msg4
nwln
PutStr msg5
nwln
PutStr msg6
GetStr    resp
mov    AL,resp
cmp 1,AL
je registros
cmp 2,AL
je memoria
cmp 3,AL
je    programa
jmp done


;--------------------------------------------------------------------------------------------------
;FUNCIONES
;---------------------------------------------------------------------------------------------------

registros:
    jmp done
memoria:


    jmp    done
programa:
    jmp    done
done:
    .Exit

















binario:
    push    eax
    push    ebx
    mov        ebx,tamaBuff
    mov        ecx,4
bin:

    ;mov        AL,byte[ebx]
    mov     AH,80H       ; mask byte = 80H
    push    ecx
    mov     ecx,8        ; loop count to print 8 bits
print_bit:
    test    byte[ebx],AH        ; test does not modify AL
    jz      print_0      ; if tested bit is 0, print it
    PutCh   '1'          ; otherwise, print 1
    jmp     skip1
print_0:
    PutCh   '0'          ; print 0
skip1:
    shr     AH,1         ; right-shift mask bit to test
                          ;  next bit of the ASCII code
    loop    print_bit
    nwln
    inc        ebx
    pop        ecx
    loop    bin
reto:
    pop    ebx
    pop    eax
    ret
