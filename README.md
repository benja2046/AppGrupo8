# AppGrupo8
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
