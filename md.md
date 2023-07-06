Insercion al Final
	
	```
	void ListaSimple::insertarFinal(T dato) {
		
		Nodo<T>* nuevo = new Nodo<T>(dato, nullptr)
		
		if (cola != nullptr)
			cola->sig = nuevo;
			
		if (cabecera == nullptr)
			cabecera = nuevo;
		
		cola = nuevo;
	}
	```