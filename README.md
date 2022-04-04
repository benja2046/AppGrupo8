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
FILE * openingFile(char *filename){
    FILE *fp;
    fp = fopen(filename,READ_ONLY);
    return fp;
}

int main(int argc, char *argv[])
{
    FILE *fp = openingFile(argv[1]);
    menu();
    printf("\nPara hacer cualquier cambio es fundamental saber el ID de los libros, por lo que, primero debes seleccionar la opcion numero 8\n");
    printf("Elige una opcion del menu (1,2,3,4,5,6,7,8)\n");
    int opcion; 

    scanf("%i",&opcion);

    switch(opcion)
    {
        case 1:
            opcion1(fp,argv[1]);
            break;
        case 2:
            opcion2(fp,argv[1]);
            break;
        case 3:
            opcion3(fp,argv[1]);
            break;
        case 4:
            opcion4(fp,argv[1]);
            break;
        case 5:
            opcion5(fp,argv[1]);
            break;
        case 6:
            opcion6(fp);
            break;
        case 7:
            printf("Gracias por visitar la libreria virtual");
            break;
      case 8:
            opcion8(argc,argv);
      default:
            printf("Algo mas que quieras hacer\n");
            main(argc,argv);
            break;
    }
    return 0;
}
void menu()
{
    printf("BIENVENIDO A LA BIBLIOTECA VIRTUAL\n Este es el menu de opciones\n");
    printf(" 1. Agregar o quitar un libro\n 2. Agregar o quitar una sede\n 3. Editar elementos de un libro\n 4. Agregar o eliminar secciones\n 5. Agregar o quitar pisos\n 6. Buscar un libro\n 7. Salir\n 8. Ver ID de los libros\n");
    return;
}
int opcion1(FILE *myfile,char *filename)
{
    int opcion;
    printf(" 1. Agregar un libro\n 2. Quitar un libro\n 3. Volver\n");
    printf("Elige una opcion\n");
    scanf("%i",&opcion);
    switch(opcion)
    {
        case 1:
            printf("¿Que libro desea agregar?\n");
            agregar_libro(myfile);
            break;
        case 2:
            
            quitar_libro(myfile,filename);

            break;
        case 3:
            //main();
            break;
        default:
            printf("Ups, esa opcion no esta, intenta con otra\n");
            opcion1(myfile,filename);
            break;

    }
    return 0;
}
int opcion2(FILE *myfile,char *filename)
{   
    int opcion;
    printf(" 1. Agregar una sede\n 2. Quitar una sede\n 3. Volver\n");
    printf("Elige una opcion: \n");
    scanf("%i",&opcion);
    switch(opcion)
    {
        case 1:
            printf("Para agregar una nueva sede debes rellenar todos los campos del libro\n");
            agregar_libro(myfile);
            printf("\n¡Sede agregada con exito!");
            break;
        case 2:
          
            quitar_sede(myfile,filename);
            break;
        case 3:
            //main();
            break;
        default:
            printf("Ups, esa opcion no esta, intenta con otra\n");
            opcion2(myfile,filename);
            break;

    }
    return 0;
}

int opcion3(FILE *myfile,char *filename)
{
    int opcion;
    printf("1. ¿Estas seguro de querer editar el libro? (Ingresa 1 para si y 2 para no)");
    printf("Elige una opcion\n");
    scanf("%i",&opcion);
    switch(opcion)
    {
        case 1:
            printf("\n ¡A continuacion podras cambiar todos los parametros del libro que desees editar! Si no quieres cambiar alguno de estos, debes ingresar los valores ya existentes en los campos solicitados\n");
            editar_libro(myfile,filename);
            
            
            break;
        case 2:
            break;
        default:
            printf("Ups, esa opcion no esta, intenta con otra\n");
            opcion3(myfile,filename);
            break;

    }
    return 0;
}
int opcion4(FILE *myfile,char *filename)
{
    int opcion;
    printf(" 1. Agregar una seccion\n 2. Quitar un seccion\n 3. Volver\n");
    printf("Elige una opcion\n");
    scanf("%i",&opcion);
    switch(opcion)
    {
        case 1:
            printf("Para agregar una sección debes rellenar todos los campos del libro\n");
            agregar_libro(myfile);
            printf(" \ns¡Seccion agrgada con exito!");
            break;
        case 2:
            quitar_seccion(myfile,filename);
            break;
        case 3:
            break;
        default:
            printf("Ups, esa opcion no esta, intenta con otra\n");
            opcion4(myfile,filename);
            break;

    }
    return 0;
}

int opcion5(FILE *myfile,char *filename)
{
    int opcion;
    printf(" 1. Agregar un piso\n 2. Quitar un piso\n 3. Volver\n");
    printf("Elige una opcion:\n");
    scanf("%i",&opcion);
    switch(opcion)
    {
        case 1:
            printf("Para agregar un piso debes rellenar todos los campos del libro\n");
            agregar_libro(myfile);
            printf("\n¡Piso agregado con exito!");
            break;
        case 2:
            quitar_piso(myfile,filename);
            break;
        case 3:
            break;
        default:
            printf("Ups, esa opcion no esta, intenta con otra\n");
            opcion5(myfile,filename);
            break;

    }
    return 0;
}

void opcion6(FILE *myfile)
{
    buscar_libro(myfile);
}


void opcion8(int argc, char *argv[])
{
  FILE *fp = openingFile(argv[1]);
  libro_index(fp);
  int opcion;
  printf("\n¿Quieres volver al menu?(Ingresa 1 para si y 2 para no)\n");
  scanf("%i",&opcion);
  switch(opcion)
  {
    case 1:
    main(argc,argv);
    case 2:
      break;
    default:
      printf("hola");
      opcion8(argc,argv);
      break;
  
    
      }  
    return;
    }

int agregar_libro(FILE *myfile)
{

    char libro[70],autor[50],seccion[50],edificio[4],sede[50];
    int anio,nestante,piso;

    if (!myfile) {
        printf("Can't open file\n");
        return 0;
    }
    printf("\nIngresa el nombre del libro (Los espacios se ingresan con guión bajo): \n");
    scanf("%s", &libro);
    printf("\nIngresa el nombre del autor:\n");
    scanf("%s", &autor);
    printf("\nIngresa el año del libro:\n");
    scanf("%d", &anio);
    printf("\nIngresa el numero del estante donde esta el libro:\n");
    scanf("%d", &nestante);
    printf("\nIngresa el tipo de seccion del libro:\n");
    scanf("%s", &seccion);
    printf("\nIngresa el piso donde esta el libro: \n");
    scanf("%d", &piso);
    printf("\nIngresa el edificio donde esta el libro:\n");
    scanf("%s", &edificio);
    printf("\nIngresa la sede donde esta el libro:\n");
    scanf("%s", &sede);

    fprintf(myfile, "%s, %s, %d,%d,%s,%d,%s,%s\n", libro,autor, anio,nestante,seccion,piso,edificio,sede);

    printf("\n¡Nuevo libro agregado con exito!");

    fclose(myfile);
    return 0;
}

int buscar_libro(FILE *myfile)
{
    int index = 0;

    if (myfile == NULL){
        perror("El archivo está vacío");
        exit(1);
    }

    display_info(myfile);


}

void libro_index(FILE *myfile){
    printf("\n");
    int threlin = 0;
    char linea[200];

    for (int i = 0 ;fgets(linea, sizeof(linea), myfile);i++)
    {
        char *token;
        token = strtok(linea, "," );
        if (i != 0){
            if (threlin == 3){
                printf("\n\n");
                threlin = 0;
            }
            if(i < 10){
                printf("[0%i]%s      ",i,token);
            }
            else{
                printf("[%i]%s      ",i,token);
            }

            threlin++;
        }
    }
    fclose(myfile);
}

void display_info (FILE *myfile)
{
    printf("\n\n");
    int id;
    char linea[1024];
    printf("BUSCAR LIBRO POR ID\n\n");
    printf("Ingresa el ID del libro: ");
    scanf("%i",&id);
    printf("\n");
    if (myfile == NULL){
        perror("El archivo está vacío");
        exit(1);
    }

    printf("|  ID  |  TITULO  |  AUTOR  |  AÑO  |  NºESTANTE  |  SECCIÓN  |  PISO  |  EDIFICIO  |  SEDE  |\n\n");
    for (int k = 0; fgets(linea, sizeof(linea), myfile); k++)
    {
        char *token;
        token = strtok(linea, "," );

        if (k == id){
            printf("[%i]",id);

            while (token != NULL)
            {
                printf(" , ");
                printf("%s",token);
                token = strtok(NULL,",");
            }
        }
    }
    fclose(myfile);
}


int quitar_libro(FILE *myfile,char *filename)
{
    FILE* file, *temp;
    
    char temp_filename[FILENAME_SIZE];
    char buffer[MAX_LINE];
    int delete_line =0;

    file =myfile;
    strcpy(temp_filename, "temp____");
    strcat(temp_filename, filename);

    printf("\nIngresa el ID del libro que quieres eliminar(Al ingresae esl valor del ID sumele 1 a este, si el valor es de una unidad ignore el cero que se encuentra antes de este): ");
    scanf("%d", &delete_line);

    
    temp = fopen(temp_filename, "w");

    if(myfile== NULL || temp ==NULL)
    {
        printf("error");
        return 1;
    }

    bool keep_reading =true;
    int current_line =1;
    do
    {
        fgets(buffer, MAX_LINE, file);
        if (feof(file)) keep_reading=false;
        else if (current_line != delete_line)
            fputs(buffer,temp);

        current_line++;


    } while (keep_reading);

    fclose(file);
    fclose(temp);

    remove(filename);
    rename(temp_filename, filename);
    printf("¡Libro eliminado con exito!");
    return 0;

}


int editar_libro (FILE *myfile,char *filename){
    
        FILE* file, *temp;
    
    char temp_filename[FILENAME_SIZE];
    char buffer[MAX_LINE];
    int delete_line =0;

    file =myfile;
    strcpy(temp_filename, "temp____");
    strcat(temp_filename, filename);

    printf("\nIngrese el ID del libro que quiere eliminar(Al ingresae esl valor del ID sumele 1 a este, si el valor es de una unidad ignore el cero que se encuentra antes de este): ");
    scanf("%d", &delete_line);

    
    temp = fopen(temp_filename, "w");

    if(myfile== NULL || temp ==NULL)
    {
        printf("error");
        return 1;
    }

    bool keep_reading =true;
    int current_line =1;
    do
    {
        fgets(buffer, MAX_LINE, file); 
        if (feof(file)) keep_reading=false;
        else if (current_line != delete_line)
            fputs(buffer,temp);

        current_line++;

    } while (keep_reading);
    
    char libro[70],autor[50],seccion[50],edificio[4],sede[50];
    int anio,nestante,piso;
  
    printf("Ingresa los nuevos datos del libro:");
  
    printf("\nIngresa el nombre del libro (Los espacios se ingresan         con guión bajo)\n");
    scanf("%s", &libro);
    printf("\nIngresa el nombre del autor\n");
    scanf("%s", &autor);
    printf("\nIngresa el año del libro\n");
    scanf("%d", &anio);
    printf("\nIngresa el numero del estante donde quieres que este el libro\n");
    scanf("%d", &nestante);
    printf("\nIngresa la seccion donde quieres que este el libro\n");
    scanf("%s", &seccion);
    printf("\nIngresa el piso donde quieres que este el libro \n");
    scanf("%d", &piso);
    printf("\nIngresa el edificio donde quieres que este el libro\n");
    scanf("%s", &edificio);
    printf("\nIngresa la sede donde quieres que este el libro\n");
    scanf("%s", &sede);

    fprintf(temp, "%s, %s, %d,%d,%s,%d,%s,%s\n", libro,autor, anio,nestante,seccion,piso,edificio,sede);

    printf("\n¡Libro editado!");
    
    fclose(file);
    fclose(temp);
    
    remove(filename);
    rename(temp_filename, filename);

    return 0;

}

int quitar_sede (FILE *myfile,char *filename){
  char sede;
  int opcion;
  printf("Nombre de la sede que desea eliminar: \n");
          scanf("%s",&sede);
  printf("La sede %s tiene libros asociados por lo que no se puede eliminar. Si deseas eliminar la sede debes borrar sus los libros asociados\n",&sede);
  printf("¿Quieres volver al paso 1? (si=1, no =2): \n");
  scanf("%i",&opcion);
  switch(opcion){
    case 1:
        opcion1(myfile,filename);
    case 2:
        break;
    default:
        printf("Ups, esa opcion no esta, intenta con otra\n");
            quitar_sede(myfile,filename);
    
  }
    
  return 0;
}

int quitar_seccion (FILE *myfile,char *filename){
  char seccion;
  int opcion;
  printf("Nombre de la seccion que desea eliminar: \n");
  scanf("%s",&seccion);
  printf("La seccion %s tiene libros asociados por lo que no se puede eliminar. Si deseas eliminar la seccion debes borrar sus los libros asociados\n",&seccion);
  printf("¿Quieres volver al paso 1? (Ingresa 1 para si y 2 para no: \n");
  scanf("%i",&opcion);
  switch(opcion){
    case 1:
        opcion1(myfile,filename);
    case 2:
        break;
    default:
        printf("Ups, esa opcion no esta, intenta con otra\n");
            quitar_seccion(myfile,filename);
    
  }
    
  return 0;
}

int quitar_piso (FILE *myfile,char *filename){
  int piso;
  int opcion;
  printf("Ingrese el piso que desea eliminar: \n");
  scanf("%d",&piso);
  printf("El piso %c tiene libros asociados por lo que no se puede eliminar. Si deseas eliminar este piso debes borrar sus los libros asociados\n",piso);
  printf("¿Quieres volver al paso 1? (Ingresa 1 para si y 2 para no): \n");
  scanf("%i",&opcion);
  switch(opcion){
    case 1:
        opcion1(myfile,filename);
    case 2:
        break;
    default:
        printf("Ups, esa opcion no esta, intenta con otra\n");
            quitar_piso(myfile,filename);
    
  }
    
  return 0;
}
