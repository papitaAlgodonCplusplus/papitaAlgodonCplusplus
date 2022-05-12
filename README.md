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

Google test:
1- Click derecho sobre la solucion arriba arriba
2-Agregar
3-Nuevo proyecto
4-Por defecto sale Google test, continuar
5-Se pone nombre y crear
#include "X.h"
class XTest : public ::testing::Test
{
protected:
           bool finDePruebas = false; //Para que el destructor solo destruya cuando terminen las pruebas
           variables globales que usen los test;
           X(); //Tanto esto como SetUp se ejecutan al principio de cada test
	   ~X() override; //Tanto esto como TearDown se ejecutan al final de cada test
           void SetUp() override;
           void TearDown() override;
};
XTest::X(){ //Se definen las variables globales}
XTest::~X(){//Se borra memoria, para no ocasionar problemas agregar if(finDePruebas){.....}}
void  XTest::SetUp() {}
void  XTest::TearDown() {}
//Un test de ejemplo
TEST_F(XTest, ChaChaCha){
EXPECT_EQ(1, 1);
}
//¡¡¡Esta prueba falla al proposito!!!, lo unico que hace es indicar que las pruebas reales terminaron
TEST_F(XTest, Terminar) {
	finDePruebas = true;
}
//EXPECT_TRUE(bool x);
//EXPECT_FALSE(bool x);
//EXPECT_EQ(int a, int b)  a == b
//EXPECT_NE(int a, int b)  a != b
//EXPECT_LT(int a, int b)  a < b
//EXPECT_LE(int a, int b)  a <= b
//EXPECT_GT(int a, int b)  a > b
//EXPECT_GE(int a, int b)  a >= b
//Para ASSERT, solo cambiar EXPECT por ASSERT (Que es como para mas obligatoriedad)
	
Agregar estructuras apuntadas por shared_ptr por orden numérico:
//REQ: Estructura X tenga puntero a siguiente sg y la clase un puntero a inicio de estructura
	bool encontrado = false; //indica si ya encontramos la posicion en donde colocamos
	shared_ptr<X> p = inicio; //apuntador al inicio
	shared_ptr<X > aux = 0; //como un auxiliar
	if (inicio == 0) { //Si no hay nada en el inicio, agregamos aqui
		inicio = shared_ptr<X>(new X(numeroagregando));
		encontrado = true;
	}
	else if (inicio->numero> numeroagregando) { //En caso de que se ocupe poner antes de inicio
		p = shared_ptr<X>(new X(numeroagregando));     // Se crea el nuevo X
		p->sg = inicio;         // Se reespalda el numero del inicio
		inicio = p;              // Ponemos el nuevo X en orden
		encontrado = true;
	}
	else {                       // Si no esta al inicio, ni antes del inicio, buscamos el X de referencia
		p = inicio;
		while (p != 0) {
			if (p->numero == numeroagregando)   //Si ya existía el numero entonces no hacemos nada
				p = 0;
			else { // Seguimos buscando
				if (p->numero <numeroagregando) { //Si nuestro numero esmayor al ultimo encontrado, va despues
					aux = p;
					p = p->sg;
					if (p == 0) // Si no hay un numero luego, se agrega al final
						encontrado = true;
				}
				else { //Si p->numero > numeroagregando, solo la ponemos antes de p
					p = 0;
					encontrado = true; // hay que agregarlo
				}
			}
		}
		if (encontrado) { //Una vez determinado donde va, solo lo colocamos
			p = aux->sg;
			aux->sg= shared_ptr<X>(new X(numeroagregando));
			aux->sg->sg = p;
		}
	}
