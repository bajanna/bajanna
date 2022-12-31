.MODEL SMALL
.DATA
        VAL1         DB      ?
        DISPLAY1     DB      0AH,0DH,'NUMBER OF SUBJECTS :','$'
        DISPLAY2         DB      0AH,0DH,'ENTER GRADE:','$'
        DISPLAY3         DB      0AH,0DH,'AVEARGE:','$'
    BUFFER       DB      3,4 DUP(?)
.CODE
MAIN    PROC

.STARTUP

        LEA DX,DISPLAY1 
        MOV AH,09H  
        INT 21H

        MOV AH,01H  
        INT 21H
        SUB AL,30H

        MOV CL,AL
        MOV BL,AL   
        MOV AL,00  
        MOV VAL1,AL 

LBL1:
        LEA DX,DISPLAY2 
        MOV AH,09H
        INT 21H

        MOV AH,0AH  
        LEA DX,BUFFER
        INT 21H
        SUB AL,30H

        ADD AL,VAL1 
        MOV VAL1,AL 
        LOOP LBL1   

LBL2:
        LEA DX,DISPLAY3 
        MOV AH,09H
        INT 21H

        MOV AX,00   
        MOV AL,VAL1 
        DIV BL      
        ADD AX,3030H    
        MOV DX,AX   
        MOV AH,02H  
        INT 21H
        
        MOV AH,4CH
        INT 21H

.EXIT

MAIN    ENDP
        END     MAIN
