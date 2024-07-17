# wc en c 
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CHAR 1000

void wc_def(FILE* file,char** filename);
void optionManager(FILE* file,char* argv[],int argc);

int main (int argc,char* argv[]){
	FILE* file=NULL;
	optionManager(file,argv,argc);
	return 0;
}

void wc_def(FILE* file,char* argv[]){
	file=fopen(argv[1],"r");
	if (file==NULL){
		perror("Erreur lors de l'ouverture du fichier\n");
		return;
	}
	int t,c=0,w=0,l=0;
	char word[MAX_CHAR];
	//char line[500];
	while ((t=fgetc(file)) != EOF){
		c++;
		if(t=='\n'){
			l++;
		}
	}
	rewind(file);
	while ((fscanf(file, "%s", word) != EOF)){	
		w++;
	}
	printf(" %d %d %d %s\n",l,w,c,argv[1]);
	fclose(file);
}

void optionManager(FILE* file,char* argv[],int argc){
	if (argc < 2){
		printf("Utilisation: %s -<option> <fichier>\n",argv[0]);
	}
	else if (argc == 2){
		wc_def(file,argv);
	} 
	else if (argc > 2){
		///Options
		// -w (word number)
		if (strcmp(argv[1],"-w")==0){
			file=fopen(argv[2],"r");
			if (file==NULL){
				perror("Erreur lors de l'ouverture du fichier\n");
				return;
			}
			int w=0;
			char word[MAX_CHAR];
			while ((fscanf(file, "%s", word) != EOF)){	
				w++;
			}
			printf("%d %s\n",w,argv[2]);
			fclose(file);
		}
		// -l (line number)
		if (strcmp(argv[1],"-l")==0){
			file=fopen(argv[2],"r");
			if (file==NULL){
				perror("Erreur lors de l'ouverture du fichier\n");
				return;
			}
			int t,l=0;
			while ((t=fgetc(file)) != EOF){
				if(t=='\n'){
					l++;
				}
			}
			printf("%d %s\n",l,argv[2]);
			fclose(file);
		}
		// -m (char number)
		if (strcmp(argv[1],"-m")==0){
			file=fopen(argv[2],"r");
			if (file==NULL){
				perror("Erreur lors de l'ouverture du fichier\n");
				return;
			}
			int t,c;
			while ((t=fgetc(file)) != EOF){
				c++;
			}
			printf("%d %s\n",c,argv[2]);
			fclose(file);
		}
		// -c (bit count)
		if (strcmp(argv[1],"-c")==0){
			file=fopen(argv[2],"r");
			if (file==NULL){
				perror("Erreur lors de l'ouverture du fichier\n");
				return;
			}
			int t,c;
			while ((t=fgetc(file)) != EOF){
				c++;
			}
			printf("%d %s\n",c,argv[2]);
			fclose(file);
		}
		// -L (maximum display length)
		if (strcmp(argv[1],"-L")==0){
			file=fopen(argv[2],"r");
			if (file==NULL){
				perror("Erreur lors de l'ouverture du fichier\n");
				return;
			}
			char line[MAX_CHAR];
                        int max_length = 0;
                        while (fgets(line, MAX_CHAR, file)) {
                            int length = strlen(line);
                            if (length > max_length) {
                                max_length = length;
                            }
                        }
                        printf("%d %s\n", max_length-1, argv[2]);
			fclose(file);
		}
	}
}
```
## Ismaël 
