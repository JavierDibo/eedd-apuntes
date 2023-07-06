# Preguntas tipo test por temas

---

## Tema 3

1. [V] La siguiente declaración: `int** p` permite crear las siguientes estructuras de datos en memoria:
	- Se crea:
		- un puntero simple a simple (`**p = 1`)
			```cpp
			p = new int*;
			*p = new int;
			```
		- un array de punteros (`*p[i] = 1`)
			```cpp
			p = new int*[];
			for(): p[i] = new int;
			```
		- un array a un array (`p[i][j] = 1`)
			```cpp
			p = new int*[];
			for(): p = new int[];
			```

2. [V] Si la declaración del puntero anterior `p` se realiza como se muestra a continuación entonces `p` es creado como una variable residente en la pila de aplicación:

	```cpp
	void f() {
		int **p;
		...
	}
	```
	
	Las declaraciones automáticas se realizan en la pila.

3. [V] Una matriz declarada como `int a[3][5]` se almacena en una zona contigua de memoria.

	Las matrices son reservadas al mismo tiempo en zonas contiguas.

4. [V] Sea `m1` una matriz declarada como `int m1[10][20]` y `m2` un puntero declarado como `int **m2` e iniciado mediante el siguiente código:

	```cpp
	m2 = new int*[10];
	for (int c = 0; c < 10; ++c) {
		m2[c] = new int[20];
	}
	```
	
	Entonces el elemento existente en la posición (3, 7) se accede de igual manera con ambas estructuras de datos: `m1[3][7] / m2[3][7]`.
	
	Verdadero, las dos declaraciones son equivalentes, por lo tanto, su forma de acceso también.

5. [V] El siguiente código presenta memory leaks:

	```cpp
	int *p = new int[1000];
	for (int c = 0; c <= 1000; ++c) {
		p[c] = 0;
	}
	```

	Verdadero. Si se asume que este es todo el código, entonces no se libera la memoria y por lo tanto existe un memory leak. Además, se presenta un heap overflow (c <= 1000).

6. [F] El siguiente código presenta heap overflows:
	
	```cpp
	int *p;
	for (int c = 0; c < 10; ++c) {
		p = new int[100];
	}
	```
	
	Falso. No se está intentando acceder a memoria sin reservar. Lo que está ocurriendo es un memory leak. No se está usando `delete[]`.

7. [V] Una plantilla de clase instanciable para el tipo `T = int` puede que no lo sea para el tipo `T = MiClase`, es decir, que una plantilla puede no aceptar cualquier tipo como parámetro.

	Verdadero. Si la clase es muy distinta en sus operadores, por ejemplo una clase Matriz, la plantilla no funcionaría correctamente.

8. [V] A través del puntero `int **m` podemos manejar una matriz creada en memoria dinámica con un número de

filas y columnas arbitrario.

	Verdadero. Se puede declarar una matriz de cualquier tamaño usando memoria dinámica (`new`) con el código:

	```cpp
	m = new int*[p];
	for (int i=0; i<p; i++)
		m[i] = new int[q];
	```

---

## Tema 4

1. [V] Un vector dinámico es una estructura de datos básica que puede ser utilizada en la implementación de asociaciones y composiciones múltiples cuando no hay restricciones o necesidades especiales en las mismas.

	Verdadero. Es una estructura versátil que puede usarse para la mayoría de relaciones entre clases debido a su inserción en O(1) al final.

2. [F] Un dato almacenado en un vector dinámico que permanece en dicha estructura de datos a lo largo de todo su ciclo de vida nunca cambia su posición de memoria.

	Falso. Se puede dar que el mismo dato cambie de array y, por tanto, de posición de memoria cuando el vector disminuye/aumenta de tamaño en el paradigma de vectores dinámicos estudiado.

3. [V] La siguiente definición de vector estático necesita de constructor copia y operador de asignación:

	```cpp
	template<typename T> class MiVect {
		int tama;
		T *v;
	public:
		MiVect(int n) {
			tama = n;
			v = new T[tama];
		}
		...
	};
	```

	Verdadero. Toda estructura de datos completa necesita un constructor de copia y un operador de asignación para poder hacer uso de los recursos dinámicos automáticos de C++.

4. [F] La misma clase anterior debe definir así el operador corchete “[ ]” para que funcione correctamente (se obvian las comprobaciones de rango):

	```cpp
	T operator[](unsigned i) { 
		return v[i]; 
	}
	```
	
	Falso. El operador corchete debe devolver una referencia al objeto, no una copia.

5. [F] Si se ha instanciado en la clase Biblioteca a `Mivect` para implementar una relación de asociación con la clase Libro como:

	```cpp
	MiVect<Libro*> estante;
	```
	
	Entonces el destructor de Biblioteca debe entonces eliminar estante ejecutando:
	
	```cpp
	delete[] estante;
	```

	Falso. La asociación implica utilizar objetos ya existentes con un ciclo de vida independiente. La clase Biblioteca no tiene que eliminar `estante`.

6. [V] Es posible eliminar una posición de un vector dinámico en tiempo O(1) si no es necesario preservar el orden de los datos.

	Verdadero. Se intercambia el valor del objeto final con el objeto en la posición a eliminar en O(1).

7. [F] La implementación normal de un vector dinámico implementa una reducción del tamaño físico `tamf` a la mitad cuando el tamaño lógico `taml` cae por debajo de `tamf/2`.

	Falso. Esta reducción sucede cuando el tamaño lógico es 1/3 del tamaño físico.

---

## Tema 5

1. [V] El operador de asignación de la clase `Matriz<T>::operator=` debe siempre destruir la matriz destino de la asignación.

	Verdadero.

La implementación del operador de asignación debe liberar la memoria de la matriz destino antes de realizar la asignación.

2. [F] El operador de la clase `Matriz<T>::operator+=` devuelve el objeto resultado por copia.

	Falso. Estos operadores devuelven una referencia al objeto.

3. [F] La implementación de conjuntos mediante vectores realiza la intersección en tiempo lineal.

	Falso. La intersección se realiza comprobando la existencia de cada número en A dentro de B, es decir, O(n^2).

4. [V] El problema que poseen los conjuntos de bits es que el ID de un elemento debe ser un entero desde 0 hasta el tamaño del conjunto - 1. Para convertirlo en un ID genérico se necesita otra EEDD.

	Verdadero. Los objetos están codificados en números enteros, donde n/8 se refiere a su byte, y n%8 a su bit. Cada conjunto debe recibir nombres con valores numéricos enteros. Se tiene que usar otra EEDD, como un par, para asociar una etiqueta.

5. [F] Para almacenar 3841 datos en un conjunto de bits, debo crear un buffer de 480 bytes.

	Falso. `480 * 8 = 3840`, necesitamos un byte extra para almacenar el siguiente bit (dato).

6. [F] `a.intersec(b+a) == a` es correcto.

	Falso. No se puede determinar su validez sin más información. La implementación de los operadores y las definiciones de las variables `a` y `b` son necesarias para evaluar la veracidad de esta afirmación.

7. [F] El resultado de realizar esta operación: `char mascara = 1 << (500 % 8);` es `00000100`.

	Falso. El operador `<<` mueve un bit la cantidad de pasos indicados a la izquierda, es decir, 4 (500%8) pasos. El resultado sería: `00010000`.