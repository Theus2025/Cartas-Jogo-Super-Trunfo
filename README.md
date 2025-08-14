#include <stdio.h>
#include <string.h>

// Definição da estrutura para armazenar os dados de uma carta da cidade
struct CartaCidade {
    char estado[3];       // Sigla do estado (ex: "SP")
    int codigo;           // Código da cidade
    char nome[50];        // Nome da cidade
    long long populacao;  // População da cidade
    long long pib;        // PIB da cidade em reais
    double area;          // Área da cidade em km²
    int pontosTuristicos; // Número de pontos turísticos
    double densidade;     // Densidade populacional (calculada)
    double pibPerCapita;  // PIB per capita (calculado)
};

// Protótipo da função para registrar uma carta da cidade
void registrarCarta(struct CartaCidade *carta);

int main() {
    // Declaração de uma variável do tipo CartaCidade
    struct CartaCidade minhaCarta;

    // Chamada da função para registrar os dados na carta
    registrarCarta(&minhaCarta);

    // Imprimindo as informações da carta da cidade
    printf("\n--- Informações da Carta da Cidade ---\n");
    printf("Estado: %s\n", minhaCarta.estado);
    printf("Código: %d\n", minhaCarta.codigo);
    printf("Nome da Cidade: %s\n", minhaCarta.nome);
    printf("População: %lld habitantes\n", minhaCarta.populacao);
    printf("PIB: R$ %lld\n", minhaCarta.pib);
    printf("Área: %.2f km²\n", minhaCarta.area);
    printf("Pontos Turísticos: %d\n", minhaCarta.pontosTuristicos);
    printf("Densidade Populacional: %.2f hab/km²\n", minhaCarta.densidade);
    printf("PIB Per Capita: R$ %.2f\n", minhaCarta.pibPerCapita);

    return 0;
}

// Função para registrar os dados em uma carta da cidade
void registrarCarta(struct CartaCidade *carta) {
    printf("--- Registro da Carta da Cidade ---\n");

    // Coletando os dados da cidade
    printf("Digite a sigla do estado (ex: SP): ");
    scanf("%s", carta->estado);

    printf("Digite o código da cidade: ");
    scanf("%d", &carta->codigo);

    // Limpando o buffer de entrada para evitar problemas com o fgets
    getchar();

    printf("Digite o nome da cidade: ");
    fgets(carta->nome, sizeof(carta->nome), stdin);
    // Remove o '\n' adicionado pelo fgets
    carta->nome[strcspn(carta->nome, "\n")] = '\0';

    printf("Digite a população da cidade: ");
    scanf("%lld", &carta->populacao);

    printf("Digite o PIB da cidade (em R$): ");
    scanf("%lld", &carta->pib);

    printf("Digite a área da cidade (em km²): ");
    scanf("%lf", &carta->area);

    printf("Digite o número de pontos turísticos: ");
    scanf("%d", &carta->pontosTuristicos);

    // Verificação para evitar divisão por zero
    if (carta->area > 0) {
        // Cálculo da densidade populacional
        carta->densidade = (double)carta->populacao / carta->area;
    } else {
        carta->densidade = 0.0;
    }

    if (carta->populacao > 0) {
        // Cálculo do PIB per capita
        carta->pibPerCapita = (double)carta->pib / carta->populacao;
    } else {
        carta->pibPerCapita = 0.0;
    }

    printf("\nCarta da cidade registrada com sucesso!\n");
}
