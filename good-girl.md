## GOOD GIRL
Encontré este reto en la página [crackmes.one](https://crackmes.one)

<img width="1241" height="561" alt="image" src="https://github.com/user-attachments/assets/88803624-c84e-4a1e-9033-43161c711fb5" />

Con el comando `fille` podemos obtener mayor información acerca de este binario. En esta ocasión el binario que tenemos es un `ELF` de `64-bit` como podemos ver en la siguiente imagen.

<img width="1892" height="140" alt="image" src="https://github.com/user-attachments/assets/00d8c323-84da-48c3-b1f2-150fc82ffd9f" />

Algo importante que tenemos que observar es que el resultado del comando `file` tiene la palabra `stripped` eso quiere decir que el binario no tiene símbolos ("Identificadores" o "símbolos" son los nombres que se proporcionan para variables, tipos, funciones y etiquetas en el programa.)  

<img width="1900" height="128" alt="image" src="https://github.com/user-attachments/assets/8c695633-e4ed-4455-b799-d8b9fdb0f88d" />

Ejecutamos el binario para saber qué entrada nos pide.
Como podemos observar, en la imagen de abajo, cuando se ejecuta el programa nos muestra como salida el texto "bad girl!".

<img width="1900" height="60" alt="image" src="https://github.com/user-attachments/assets/88caa9cc-3acf-40a8-b9ea-1ee106ffa84d" />

Con esa información, abirmos nuestro desensamblador. En este caso estaré usando IDA FREE porque no me gusta Ghidra. Una vez abierto, lo primero que me gusta hacer es buscar el texto de salida que vimos en nuestro programa.
Para esto nos vamos a `View > Open subviews > strings` como se muestra en la imagen de abajo.

<img width="1900" height="543" alt="image" src="https://github.com/user-attachments/assets/cc05b3b6-e6c5-49e7-bdb7-9cd6b412fc43" />

Una vez habilitada esta vista, podremos ver todas las cadenas que contiene nuestro programa. Como podemos ver, encontramos nuestra cadena (1) `bad girl!` y además hay otra cadena (2) `good girl!` que es el texto más probable que tenemos que mostrar.

<img width="1900" height="640" alt="image" src="https://github.com/user-attachments/assets/3b96a38b-e618-4b96-90ba-26d91d67b57d" />

Hacemos doble click en un texto que queremos ver para que no lleve a la sección en la que está almacenado. Podemos ver que las dos cadenas de texto están en la sección `.rodata`

<img width="1900" height="640" alt="image" src="https://github.com/user-attachments/assets/dc8be3f2-3ad8-4e81-93cb-5d0ba5c1455a" />

Para los que son nuevos en reversing el segmento `.rodata` contiene constantes. La forma de acceder a estas constantes en x64 es através de `RIP Adressing` (Relative Instruction Pointer Addressing) En la imagen de abajo en (1) podemos ver como se accede a una de las constantes en el segmento `.rodata`

<img width="1340" height="105" alt="image" src="https://github.com/user-attachments/assets/1607fc46-83fb-43dd-9c39-3fe7c25f413d" />

Consultando la siguiente página podemos obtener información acerca de los opcodes de la instrucción `movdqa` [shell-storm](https://shell-storm.org/x86doc/)



```
66 0F 6F 05 A5 0F 00 00 
```
En la imagen de abajo podemos ver los opcodes de la instrucción.

<img width="1894" height="83" alt="image" src="https://github.com/user-attachments/assets/b720a9cb-744f-42ab-9482-6ba2f5f96c94" />
