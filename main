#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#ifdef _WIN32 //  _WIN64
#include <Windows.h>
#else
#include <unistd.h>
#endif

int *encontra_letra(const char *word, const char letter);
int escolhe_letra(const char letter);
void revela_letra(const char *word_orig, char *word_ocult, const int *pos);
void lower_case(char *word);
void limpar();
void update();
void esperar(int time);

int vidas = 5;

char *palavra_oculta;

char *palavra_revelada;

char *letras_escolhidas;

int main(int argc, char *argv[])
{
	char letra;

	//aloca memoria para todas as letras do alfabeto + 1
	letras_escolhidas = malloc(27 * sizeof(char));

	//aloca memoria para a palavra que deve ser adivinhada
	palavra_oculta = malloc(21 * sizeof(char));

	printf("Escreva uma palavra de até 20 letras:");
	scanf("%s", palavra_oculta);

	//Deixa a palavra inteira com letras minusculas
	lower_case(palavra_oculta);

	//aloca memoria para o ponteiro que guarda a posição da letra escolhida
	int *pos_letra = malloc((strlen(palavra_oculta) + 1) * sizeof(int));

	//limpa o terminal
	limpar();

	//aloca memoria para a palavra oculta
	palavra_revelada = malloc((strlen(palavra_oculta) + 1) * sizeof(char));

	//preenche a variável com underline's
	for (int i = 0; i < strlen(palavra_oculta); i++)
	{
		palavra_revelada[i] = '_';
	}

	while (1)
	{
		//escreve a quantidade de vidas e a palavra oculta
		update();

		if (!strcmp(palavra_oculta, palavra_revelada))
		{
			update();
			printf("\nVocê ganhou!!\n");
			break;
		}

		if (vidas == 0)
		{
			printf("\nVocê Perdeu!\n");
			break;
		}

		printf("\nDigite uma letra: ");

		//captura o \n do buffer
		getchar();
		scanf("%c", &letra);

		//verifica se a letra é maiúscula
		if (letra <= 90 && letra >= 60)
		{
			//deixa a letra minúscula
			letra += 32;
		}

		//Verifica se a letra já foi inserida anteriormente
		if (!escolhe_letra(letra))
		{
			//registra a posição da letra
			pos_letra = encontra_letra(palavra_oculta, letra);
		}
		else
		{
			printf("Letra já escolhida anteriormente. \n");
			esperar(1);
			continue;
		}

		//verifica se há esse letra na palavra
		if (pos_letra[0] != -1)
		{
			//chama a função para escrever a letra no vetor
			revela_letra(palavra_oculta, palavra_revelada, pos_letra);
		}
		else
		{
			printf("\nNão foi dessa vez!\nA palavra não contém a letra %c\n", letra);
			vidas--;
			esperar(1);
		}
	}

	return 0;
}

int escolhe_letra(const char letter)
{
	//verifica se a letra está no vetor
	for (int i = 0; i < strlen(letras_escolhidas); i++)
	{
		if (letras_escolhidas[i] == letter)
		{
			return 1;
		}
	}

	//senão adiciona ela
	letras_escolhidas[strlen(letras_escolhidas)] = letter;

	return 0;
}

int *encontra_letra(const char *word, const char letter)
{
	int *pos = malloc((strlen(word) + 1) * sizeof(int));
	//contador da posição da lista
	int aux = 0;

	for (int i = 0; i < strlen(word); i++)
	{
		if (word[i] == letter)
		{
			pos[aux] = i;
			aux++;
		}
	}

	//adiciona um indicador de terminador
	if (aux > 0)
	{
		//o terminador fica após a última posição
		pos[aux] = -1;
	}

	if (aux == 0)
	{
		//indicador que não contém a letra na palavra
		pos[0] = -1;
	}

	return pos;
}

void revela_letra(const char *word_orig, char *word_ocult, const int *pos)
{
	for (int i = 0; pos[i] != -1; i++)
	{
		word_ocult[pos[i]] = word_orig[pos[i]];
	}
}

void limpar()
{
#ifdef _WIN32 //  _WIN64
	system("cls");
#else
	system("clear");
#endif
}

void update()
{
	limpar();
	printf("Vidas: %d\n", vidas);
	for (int i = 0; i < strlen(palavra_oculta); i++)
	{
		printf(" %c ", palavra_revelada[i]);
	}
	printf("\n");

	printf("\nLetras escolhidas: ");
	for (int i = 0; i < strlen(letras_escolhidas); i++)
	{
		printf(" %c ", letras_escolhidas[i]);
	}

	printf("\n");
}

void esperar(int time)
{
#ifdef _WIN32 // _WIN64
	Sleep(time);
#else
	sleep(time);
#endif
}

void lower_case(char *word)
{
	for (int i = 0; i < strlen(word); i++)
	{
		//verifica se o caractere é maiúsculo (código ansi)
		if (word[i] <= 90 && word[i] >= 60)
		{
			//salta 32 posições na tabela, transformando a letra maiúscula em minúscula
			word[i] = word[i] + 32;
		}
	}
}
