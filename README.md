# AppGrupo8
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
#define MAXCHAR 1000
#define READ_ONLY "a+"
void libro_index(FILE *myfile);
void display_info (FILE *myfile);

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <stdbool.h>
void menu();
int opcion1(FILE *myfile,char *filename);
int opcion2(FILE *myfile,char *filename);
int opcion3();
int opcion4(FILE *myfile,char *filename);
int opcion5(FILE *myfile,char *filename);
void opcion6(FILE *myfile);
void opcion8(int argc, char *argv[]);
int editar_libro (FILE *myfile,char *filename);
int agregar_libro(FILE *myfile);
int buscar_libro(FILE *myfile);
int quitar_libro(FILE *myfile,char *filename);
int quitar_sede (FILE *myfile,char *filename);
int quitar_seccion (FILE *myfile,char *filename);
int quitar_piso (FILE *myfile,char *filename);
#define FILENAME_SIZE 1024
#define MAX_LINE 2048
