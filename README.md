# Python_5

# -*- coding: utf-8 -*-
"""
Created on Thu Apr 24 10:07:08 2025

@author: 2240711
"""

#%%

import numpy as np


#%%

#R= {(1,1),(1,3),(2,1),(2,3),(3,1),(3,2),)(4,4)}.
MR=np.array([[1,0,1,0],[1,0,1,0],[1,1,0,0],[0,0,0,1]])


#matriz da relação inversa R^(-1)

Mrinv=MR.T

#Matriz da relação composição

Maux=MR@MR
def FiltroUm(M):
    L,C=M.shape
    for i in range (L):
        for j in range (C):
            if M[i,j]!=0:
                M[i,j]=1
                
    return M

MR2=FiltroUm(Maux)

#---------------
MR2=MR@MR
MR2[MR2!=0]=1
#---------------
MR3=MR@MR
MR3[MR2!=0]=1
#---------------

"""

R não é refelxiva pois (2,2) não pertence a R ou seja MR[1,1]=0

R não é siméterica pois a posição Mr[1,0]=1 e MR[0,1]=0 / para serem tinham que ter o mesmo valor atribuido

R não é antisimétrica pois MR[2,1]=1 e MR[1,2]=1

R não é transitiva pois MR e MR2 na posição como exemplo a MR[0,1]=0 e na MR2[0,1]=1

"""

#%%

def is_reflexiva(MR):
  
    linhas, colunas = MR.shape
 
    for i in range(linhas):
        if MR[i, i] != 1:
            return False
    return True


MR = np.array([[0, 1, 0],
               [1, 1, 1],
               [1, 0, 0]])

print(is_reflexiva(MR))  

#-------------------------

def is_simetrica(M):
    if (M==M.T).all():
        return True
    else:
        return False
    
#-------------------------

def isantissimetrica(M):
    Linhas,Colunas=M.shape
    for i in range(Linhas):
        for j in range(Colunas):
            if i!=j and M[i,j]==1 and M[j,i]==1:
                return False
    return True

#-------------------------


# -*- coding: utf-8 -*-
"""
Created on Thu May 15 10:13:01 2025

@author: 2240711
"""
import numpy as np
import pandas as pd

from numpy.linalg import matrix_power as MP

FICHEIRO = pd.ExcelFile('Matriz_Adj_Ex1.xlsx')
F1 = pd.read_excel(FICHEIRO, 'MAdj', header=None)
A=F1.to_numpy()

# caminhos de comprimento 3

A3=A@A@A


#do vértice V2 para o V6
A3[1,5]

#caminhjos de comp. menor ou igual a 4
# B4=A+A^2+A^#+A^4

B4 = A + MP(A, 2) + MP(A, 3) + MP(A, 4)

#grau de saída de vértice 3
Gsaida3=0

for i in range(6):
    Gsaida3+=A[2,i]
    
Gsaida3

#grau de entrada de vértice 3
Gsaida3=0

for i in range(6):
    Gsaida3+=A[i,2]
    
Gsaida3

#------------------------------------

for i in range(6):
    Gsaida=0
    for j in range(6):
        Gsaida+=A[i,j]
        print('vertice'+str(i+1), 'saida'+str(Gsaida))

#--------------------------------------
#matriz de caminho

soma=A
for i in range(2,7):
    soma+=MP(A,i)
P=soma
P[P!=0]=1

(P==np.ones(6).all())

