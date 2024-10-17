#include <stdio.h>
#include <stdlib.h>
#include <string.h>


typedef struct Encomenda {
    char destinatario[100];
    float distancia;
    struct Encomenda *proximo;
} Encomenda;


Encomenda *criarEncomenda(char destinatario[], float distancia) {
    Encomenda *nova = (Encomenda *)malloc(sizeof(Encomenda));
    if (nova == NULL) {
        printf("Erro ao alocar memória para nova encomenda.\n");
        exit(1);
    }
    strcpy(nova->destinatario, destinatario);
    nova->distancia = distancia;
    nova->proximo = NULL;
    return nova;
}


void inserirEncomenda(Encomenda **lista, char destinatario[], float distancia) {
    Encomenda *nova = criarEncomenda(destinatario, distancia);

    
    if (*lista == NULL || (*lista)->distancia > distancia) {
        nova->proximo = *lista;
        *lista = nova;
    } else {
        Encomenda *atual = *lista;

       
        while (atual->proximo != NULL && atual->proximo->distancia < distancia) {
            atual = atual->proximo;
        }

        nova->proximo = atual->proximo;
        atual->proximo = nova;
    }

    printf("Encomenda para %s a %.2f km inserida.\n", destinatario, distancia);
}


void removerEncomenda(Encomenda **lista, char destinatario[]) {
    if (*lista == NULL) {
        printf("Nenhuma encomenda na lista.\n");
        return;
    }

    Encomenda *atual = *lista;
    Encomenda *anterior = NULL;

  
    while (atual != NULL && strcmp(atual->destinatario, destinatario) != 0) {
        anterior = atual;
        atual = atual->proximo;
    }

    
    if (atual == NULL) {
        printf("Encomenda para %s não encontrada.\n", destinatario);
        return;
    }

   
    if (anterior == NULL) {
        *lista = atual->proximo;
    } else {
        anterior->proximo = atual->proximo;
    }

    printf("Encomenda para %s removida da lista.\n", destinatario);
    free(atual); 
}


void exibirEncomendas(Encomenda *lista) {
    if (lista == NULL) {
        printf("Nenhuma encomenda para exibir.\n");
        return;
    }

    Encomenda *atual = lista;
    printf("Encomendas na ordem de entrega (da mais próxima para a mais distante):\n");

    while (atual != NULL) {
        printf("Destinatário: %s, Distância: %.2f km\n", atual->destinatario, atual->distancia);
        atual = atual->proximo;
    }
}

int main() {
    Encomenda *lista = NULL; 
    int opcao;
    float distancia;
    char destinatario[100];

    do {
        printf("\n--- Menu ---\n");
        printf("1. Inserir nova encomenda\n");
        printf("2. Exibir encomendas\n");
        printf("3. Remover encomenda (entregue)\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);
        getchar();  

        switch (opcao) {
            case 1:
                printf("Digite o nome do destinatário: ");
                fgets(destinatario, 100, stdin);
                destinatario[strcspn(destinatario, "\n")] = '\0';  
                printf("Digite a distância até o destinatário (em km): ");
                scanf("%f", &distancia);
                inserirEncomenda(&lista, destinatario, distancia);
                break;
            case 2:
                exibirEncomendas(lista);
                break;
            case 3:
                printf("Digite o nome do destinatário da encomenda entregue: ");
                fgets(destinatario, 100, stdin);
                destinatario[strcspn(destinatario, "\n")] = '\0';  
                removerEncomenda(&lista, destinatario);
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opcao invalida!\n");
        }
    } while (opcao != 0);

    return 0;
}
