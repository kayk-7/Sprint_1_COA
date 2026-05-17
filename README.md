# Sprint 1 - Otimização de sistema nos eletropostos


**André Santos de Azevedo - RM572236**

**Bruno Menezes Monegatto -  RM570311**

**Fabiana Yumi Rodrigues Nakagawa - RM571249**

**Iago Neiva Gorrão - RM 570234**

**João Pedro Amorim Albuquerque - RM 573342**

**Kayky Araujo Silva - RM569535**

**Kelly Stephanie Mendoza - RM 569044**

Código utilizado: 


; ===================================================== ; EV CHALLENGE 2026 ; Controle otimizado para eletroposto ; Assembly x86 NASM ; =====================================================

section .data

sensor_carro db 1 
usuario_token db 1 
token_valido db 1

msg_carro db "Carro detectado", 10 
len_carro equ $ - msg_carro

msg_auth db "Usuario autenticado", 10 
len_auth equ $ - msg_auth

msg_fail db "Falha na autenticacao", 10 
len_fail equ $ - msg_fail

msg_carga db "Carga iniciada", 10 
len_carga equ $ - msg_carga

msg_fim db "Carga encerrada", 10 
len_fim equ $ - msg_fim

section .text global _start

_start:

; ========================================== ; Verifica sensor do carro ; ==========================================

mov al, [sensor_carro] 
cmp al, 1 
jne fim

; imprime "Carro detectado"

mov eax, 4 
mov ebx, 1 
mov ecx, msg_carro 
mov edx, len_carro 
int 0x80

; ========================================== ; Autenticacao ; ==========================================

mov al, [usuario_token] 
mov bl, [token_valido]

cmp al, bl 
jne auth_fail

; imprime autenticado

mov eax, 4 
mov ebx, 1 
mov ecx, msg_auth 
mov edx, len_auth 
int 0x80

jmp iniciar_carga

auth_fail:

mov eax, 4 
mov ebx, 1 
mov ecx, msg_fail 
mov edx, len_fail 
int 0x80

jmp fim

; ========================================== ; Inicia carregamento ; ==========================================

iniciar_carga:

mov eax, 4 
mov ebx, 1 
mov ecx, msg_carga 
mov edx, len_carga 
int 0x80

; ========================================== ; Simulacao de processamento leve ; ==========================================

mov ecx, 5

loop_consumo:

dec ecx 
jnz loop_consumo

; ========================================== ; Encerrar carga ; ==========================================

mov eax, 4 
mov ebx, 1 
mov ecx, msg_fim 
mov edx, len_fim 
int 0x80

fim:

mov eax, 1 
xor ebx, ebx 
int 0x80

Problema e Justificativa: Os eletropostos utilizam software de alto nível e hardware genérico para tarefas simples como autenticação do usuário, leitura de sensores e controle de carga, gerando consumo desnecessário de energia e desperdício de ciclos de CPU.

Solução: Desenvolver um módulo de controle em linguagem Assembly para rodar em microcontroladores de baixo consumo.

Arquitetura: Optamos por uma arquitetura RISC, um processador que trabalha com um conjunto reduzindo de instruções simples. 

Impacto: eletropostos consomem menos energia para funcionar, aproveitando melhor fontes renováveis como solar e eólica. 

Relação com sustentabilidade e energias renováveis: Por nossa arquitetura possuir o menor gasto de energia possível, acaba que se torna sustentável pois ela faz com que sobre energia para outros serviços. 
