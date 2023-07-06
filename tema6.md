Lista simplemente enlazada
	Contenedor secuencial
	Inserciones
		1. Principio: O(1)
		2. Intermedio: O(n)
		3. Final: O(1)
	Borrados
		1. Principio: O(1)
		2. Intermedio: O(n)
		3. Final: O(n)
	Lectura: O(n)
	NO contigua
	
Nodo
	Capsula que contiene los datos en una lista simplemente
	Dato
	Puntero al siguiente nodo
	
Estructura de una lista enlazada
	- Secuencia de nodos enlazados
	- cabecera
	- cola
	- Ultimo nodo apunta a `nullptr`

Casos especiales
	- Lista vacía
	- Lista con un solo elemento
	- Lista con dos elementos
	- (Normal) Lista con dos o más elementos

Insercion
	
	Insercion al Principio
	
	```
	Nodo<T> *nuevo = new Nodo<T>(dato, cabecera);
	
	
	
	cabecera = nuevo
	
	```
	
	Insercion al Final
	
	Insercion arbitraria
	

