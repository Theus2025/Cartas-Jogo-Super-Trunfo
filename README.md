#include <stdio.h>
#include <string.h>

#define NUM_CIDADES 2

typedef struct {
    int carta;
    char estado[3];
    int codigo;
    char nome[30];
    int populacao;
    float area;
    float pibe;
    int pontos_turisticos;
} Cidade;

// Função para exibir uma carta
void exibirCarta(Cidade c) {
    printf("Carta: %d\n", c.carta);
    printf("Estado: %s\n", c.estado);
    printf("Código: %d\n", c.codigo);
    printf("Nome: %s\n", c.nome);
    printf("População: %d\n", c.populacao);
    printf("Área: %.2f km²\n", c.area);
    printf("PIB: R$ %.2f bilhões\n", c.pibe);
    printf("Nº de Pontos Turísticos: %d\n", c.pontos_turisticos);
}

// Função principal
int main() {
    // Dados das cidades
    Cidade cidades[NUM_CIDADES] = {
        {1, "SP", 3550308, "São Paulo", 12396372, 1521.11, 799.3, 20},
        {2, "RJ", 3304557, "Rio de Janeiro", 6775561, 1200.27, 400.0, 25}
    };

    int jogador, escolha, outro, atributo, venceu = 0;

    printf("Bem-vindo ao Super Trunfo de Cidades!\n\n");

    // Sorteia cartas (fixo para 2 jogadores)
    jogador = 0;
    outro = 1;

    // Exibe a carta do jogador
    printf("Sua carta:\n");
    exibirCarta(cidades[jogador]);

    // Escolher atributo
    printf("\nEscolha o atributo para competir:\n");
    printf("1 - População\n");
    printf("2 - Área\n");
    printf("3 - PIB\n");
    printf("4 - Nº de Pontos Turísticos\n");
    printf("Digite o número do atributo: ");
    scanf("%d", &atributo);

    // Comparação
    float valor_jogador, valor_outro;
    switch(atributo) {
        case 1:
            valor_jogador = cidades[jogador].populacao;
            valor_outro = cidades[outro].populacao;
            printf("População: %d vs %d\n", (int)valor_jogador, (int)valor_outro);
            break;
        case 2:
            valor_jogador = cidades[jogador].area;
            valor_outro = cidades[outro].area;
            printf("Área: %.2f vs %.2f\n", valor_jogador, valor_outro);
            break;
        case 3:
            valor_jogador = cidades[jogador].pibe;
            valor_outro = cidades[outro].pibe;
            printf("PIB: %.2f vs %.2f\n", valor_jogador, valor_outro);
            break;
        case 4:
            valor_jogador = cidades[jogador].pontos_turisticos;
            valor_outro = cidades[outro].pontos_turisticos;
            printf("Pontos Turísticos: %d vs %d\n", (int)valor_jogador, (int)valor_outro);
            break;
        default:
            printf("Atributo inválido.\n");
            return 1;
    }

    if (valor_jogador > valor_outro) {
        printf("\nParabéns! Você venceu!\n");
        venceu = 1;
    } else if (valor_jogador < valor_outro) {
        printf("\nVocê perdeu! O outro jogador venceu.\n");
    } else {
        printf("\nEmpate!\n");
    }

    printf("\nCarta do outro jogador:\n");
    exibirCarta(cidades[outro]);
# Cartas-Jogo-Super-Trunfo