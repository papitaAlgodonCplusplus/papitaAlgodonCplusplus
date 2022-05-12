Punteros simples: pueden guardar x o x[]
X* a = Xa; //puntero de tipo X que apunta a Xa
X* a = new X[n]: //puntero de tipo X que apunta a un array de tipo X con n celdas, a[0], a[1]....
para liberar la memoria solo
delete Xa;
delete[] a;

Lectura de archivos:
main.cpp:
#include <iostream>
#include <fstream>
ifstream archivo("archivo.extencion", ios::in);
	if (!archivo)
		cout << "No se encontró el archivo" << endl;
	X a = X(archivo); //Se crea un nuevo objeto a de tipo X en el que constructor recibe archivo para operar 
X.h:
constructor:
X::X(ifstream& archivo){
      if (archivo.is_open()) {
		string n; //El string que ocupa getline
		getline(archivo, n); //obtiene la primera linea del archivo
      }
     //Para leer un archivo obteniendo datos separados por , 
                string linea; //strings que sirven para el getline
		string x;
		while (archivo >> linea) { //mientras existan lineas en archivo
			stringstream s(linea); //necesario para el getline
			while (getline(s, x, ',')) {
                        //Codigo a operar tomando x como el elemento encontrado por cada , }
                        }
}
