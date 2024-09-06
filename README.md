# AssemblyX86-TASM-Project
Project AssemblyX86 sintax TASM 
This project is written in assembly language for the x86 architecture and uses DOS interrupt calls to interact with the user and display messages on the screen.
.model small
.model small
.stack 100h

.data
    string db 255 dup(?)
    msg1 db "Enter a number: $"
    msg2 db 0Dh,0Ah,"Number is $"
    msg3 db 0Dh,0Ah,"Number of digits: $"
    msg4 db 0Dh,0Ah,"Even $"
    msg5 db 0Dh,0Ah,"Odd $"

.code
main proc
    mov ax, @data
    mov ds, ax

    ; print message asking for input
    lea dx, msg1
    mov ah, 09h
    int 21h

    ; read string until "$" is encountered
    mov si, offset string
    mov ah, 01h
input:
    int 21h
    cmp al, "$"
    je end_input
    cmp al, 8 ;ascii code for backspace
    jne nobackspace
    dec si ;decrement si so that number of digits doesn't count backspace - Without this it still prints the right number but the no. of digits is too high.
    jmp input
nobackspace:
    mov [si], al
    inc si
    jmp input
end_input:

    lea dx, msg2
    mov ah, 09h
    int 21h

    mov cx, si
    dec cx
    mov si, offset string
printnum:
    mov ah, [si]
    mov dl, ah
    mov ah, 02h
    int 21h
    inc si
    dec cx
    cmp cx, 0
    jne printnum

    mov ah, [si]
    mov dl, ah
    mov ah, 02h
    int 21h
    
    mov ax, 0
    mov dx, 0
    mov ax, [si]
    mov cx, 2
    div cx

    cmp dx, 0
    je numeven
    jmp numodd
numeven:
    lea dx, msg4
    mov ah, 09h
    int 21h
    jmp digits
numodd:
    lea dx, msg5
    mov ah, 09h
    int 21h
digits:
    ; print number of characters
    lea dx, msg3
    mov ah, 09h 
    int 21h

    mov ax, si
    sub ax, offset string
    add ax, 1
    call print_number

    ; terminate program
    mov ax, 4C00h
    int 21h
main endp

print_number proc
    mov cx, 0
    mov bx, 10

loop_start:
    cmp ax, 0
    je end_loop
    mov dx, 0
    div bx
    push dx
    inc cx
    jmp loop_start

end_loop:
    cmp cx, 0
    je end_print
    pop dx
    add dl, 30h
    mov ah, 02h
    int 21h
    dec cx
    jmp end_loop

end_print:
    ret
print_number endp
end main
 
