Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didácticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.

# Actualizar branch luego de merge de otra rama

Supongamos que se tiene una branch master de la cual derivo en 2 ramas a saber: b1 y b2 para trabajar sendos issues, luego de un tiempo en b1 se hace el  respectivo commit y se retorna a master para hacer git merge b1 (fast forward), luego se retorna a b2 a resolver el issue 2 pero ya el HEAD de master avanzo un paso.   

**¿Como actualizar la rama b2 a los cambios producto del merge de b1?**

**solución:**
`$git branch --set-upstream-to=origin/<branch> b2`

y luego:

`$git pull`

ready to kill !!!   :)
