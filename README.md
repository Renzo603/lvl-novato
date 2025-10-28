# lvl-novato
#include <stdio.h>
#include <string.h>

#define MAX_ITENS 10

// Estrutura para representar um item
typedef struct {
    char nome[50];
    char tipo[30];
    int quantidade;
} Item;

int main() {
    Item zaino[MAX_ITENS];
    int totalItens = 0;
    int opcao;

    do {
        printf("\n=== MENU ZAINO ===\n");
        printf("1.AGGIUNGI UN ITEM\n");
        printf("2.RITIRA UN ITEM\n");
        printf("3.LISTA\n");
        printf("4.ESCI\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        getchar(); // Limpa o buffer do teclado

        switch (opcao) {
            case 1:
                if (totalItens < MAX_ITENS){
                    printf("Nome do item: ");
                    fgets(zaino[totalItens].nome,sizeof(zaino[totalItens].nome),stdin);
                    zaino[totalItens].nome[strcspn(zaino[totalItens].nome, "\n")] = '\0';

                    printf("Tipo do item: ");
                    fgets(zaino[totalItens].tipo, sizeof(zaino[totalItens].tipo), stdin);
                    zaino[totalItens].tipo[strcspn(zaino[totalItens].tipo, "\n")] = '\0';

                    printf("Quantidade: ");
                    scanf("%d",&zaino[totalItens].quantidade);
                    getchar();

                    totalItens++;
                    printf("Item adicionado com sucesso!\n");
                }else{
                    printf("Zaino pieno!\n");
                }
                break;

            case 2: {
                char nomeRemover[50];
                printf("Digite o nome do item a remover: ");
                fgets(nomeRemover, sizeof(nomeRemover), stdin);
                nomeRemover[strcspn(nomeRemover, "\n")] = '\0';

                int encontrado = 0;
                for (int i = 0; i < totalItens; i++) {
                    if (strcmp(zaino[i].nome, nomeRemover) == 0) {
                        for(int j=i;j<totalItens-1; j++) {
                            zaino[j] = zaino[j + 1];
                        }
                        totalItens--;
                        encontrado = 1;
                        printf("Item removido com sucesso!\n");
                        break;
                    }
                }
                if (!encontrado) {
                    printf("Item não encontrado.\n");
                }
                break;
            }

            case 3:
                if (totalItens == 0) {
                    printf("Zaino vuoto.\n");
                } else {
                    printf("\nItens na mochila:\n");
                    printf("%-20s %-15s %-10s\n", "Nome", "Tipo", "Quantidade");
                    for (int i = 0; i < totalItens; i++) {
                        printf("%-20s %-15s %-10d\n", zaino[i].nome, zaino[i].tipo, zaino[i].quantidade);
                    }
                }
                break;

            case 4:
                printf("Zaino chiuso...\n");
                break;

            default:
                printf("Opção inválida. Tente novamente.\n");
        }
    } while (opcao != 4);

    return 0;
}
