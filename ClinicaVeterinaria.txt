/*Equipe: Nielson Ferreira
          Ronildo Ronaldo
          Sidney Patrick
          Luiz Vilar
          Gutembergue*/

#include<stdio.h>
#include<locale.h>
#include<windows.h>
#include<stdlib.h>

#define i 22	// quantia de colunas
#define j 70	// quantia de linhas

float TrocoSoma (float troco);
void trocoValidador ();			                             // IMPORTANTE:
void Posicao(int x,int y);                                   // Tudo o que começa com 'c' é pra cachorro e com 'g' é pra gato.
void Intanciar_campo(); //Desenha campo                      // Exemplo: 'gServicos();' -> Servicos para gato.
void gServicos();       //Serviços p/gato                    //          'cServicos();' -> Serviços para cachorro.
void cServicos();       //Serviços p/cachorro
void PDC();             //Menu secreto para o ADM
void AltVal();          //Função para alteração de preços
void Preco();           //Preços dos serviços
void IniciarSistema();
int Idade (int ano);
void Resulte();
void gMenu();		// Produtos e Servicos
void cMenu();		// Produtos e Servicos
void cadastro();

//Variaveis fora para que todas as funções e procedimento que nessetem, ter acesso;
// Variaveis para o "void Resulte ()" e Cadastro;
char NomeAnimal[16], raca[16], a[7];				// "a[7]" Opcao para tipo de animal
int dataDeNac,x;//variavel 'x' para alteracao dos valores no @com
float gValores[5];//Vetor dos precos pra gato
float cValores[5];//Vetor dos precos pra cachorro
float gModVal[5]={15.00,10.00,10.40,25.10,12.50};		//Vetores auxiliares para alteracao de precos
float cModVal[5]={20.00,15.00,15.40,30.10,17.50};		//Vetores auxiliares para alteracao de precos
float gValorServ,cValorServ;
float gValorProd,cValorProd;
int recursividade; // para void trocoValidador ();

int main() {
	system("color 70");

	Intanciar_campo();	// desenha o campo
	IniciarSistema ();
	cadastro();

	switch (a[0]) {
		case 'c' :
			cMenu ();
			break;
		case 'C' :
			cMenu ();
			break;
		case 'g' :
			gMenu ();
			break;
		case 'G' :
			gMenu ();
			break;
		default :
			break;
	}

	trocoValidador ();

	Posicao(13,16);
	printf("Obrigado Pela Preferencia e Volte Sempre!");

	Posicao(2,23);		// Posicao do system pause
	system("pause");

	return 0;
}

float TrocoSoma (float troco) {
	return troco = gValorServ + cValorServ + gValorProd + cValorProd;
}

float valor;
void trocoValidador () {
	float TrocoV;
	system("cls");

	if(recursividade == 1 && valor < TrocoSoma (TrocoV)) {
		Posicao(14,5);
        printf("=====Esse valor nao paga sua compra=====");
	}
	recursividade = 1;

	Intanciar_campo();
	Resulte ();

	Posicao(3,1);
	printf("Valor: R$ %.2f ", gValorServ + cValorServ + gValorProd + cValorProd);

	Posicao(13,8);
	printf("Pagamento: ");
	scanf("%f", &valor);

	if(valor >= TrocoSoma (TrocoV)) {
		if(TrocoSoma (TrocoV) != 0){
			Posicao(13,9);
			printf("Troco: R$ %.2f", valor - TrocoSoma (TrocoV));
		}
	} else {
		trocoValidador ();
	}
}

void Posicao(int x,int y) {
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),(COORD) { x,y });	// x=j (sao colunas) e y=i (sao as linhas)
}

void Intanciar_campo() {	//desenha a area do programa
	int z; // variavel auxiliar os for's

	Posicao(53,1);
	printf("Pet shop Brasil");
	for(z=0; z<j; z++) {	// Parede de cima horizontal
		Posicao(z,0);
		printf("%c",16);
	}
	for(z=0; z<i; z++) {	// Parede da direita vertical
		Posicao(j,z);
		printf("%c",31);
	}
	for(z=j; z>=0; z--) {	// Parede de baixo horizontal
		Posicao(z,i);
		printf("%c",17);
	}
	for(z=i; z>0; z--) {	// Parede da esquerda vertical
		Posicao(0,z);
		printf("%c",30);
	}

	for(z=69; z>=1; z--) {	// Parede de baixo horizontal
		Posicao(z,20);
		printf("-");
	}
	for(z=69; z>=1; z--) {	// Parede de baixo horizontal
		Posicao(z,2);
		printf("-");
	}
}

void gServicos () {
    int Tecla;

	system("cls");
	Intanciar_campo();
	Resulte();

    do{
        Posicao(3,1);
        printf("Valor: R$ %.2f ", gValorServ + gValorProd);

        Posicao(26,5);
        printf("=====Servicos=====");

        Posicao(8,8);
        printf("<1> Banho  - R$ %.2f", gValores[0]);
        Posicao(8,9);
        printf("<2> Tosa  -  R$ %.2f", gValores[1]);
        Posicao(8,10);
        printf("<3> Vacina - R$ %.2f", gValores[2]);
        Posicao(8,12);
        printf("<Delete> Zerar os servicos selecionados");
		Posicao(8,13);
        printf("<0> Voltar ao menu");

        Posicao(6,19);
        printf("Pressione 'enter' para Finalizar todas as compras");
		do{
		    Tecla = 0;
            fflush(stdin);
            Tecla = getch ();
		} while (Tecla != 49 && Tecla != 50 && Tecla != 51 && Tecla != 13 && Tecla != 224 && Tecla != 48);//ASCII: 49=1  50=2  13=Enter  224=Delete  48=0
		if(Tecla == 49){
			gValorServ += gValores[0];
		}
		if(Tecla == 50){
			gValorServ += gValores[1];
		}
		if(Tecla == 51){
			gValorServ += gValores[2];
		}
		if(Tecla == 48){
			gMenu ();
		}
		if(Tecla ==224){
			gValorServ = 0;
		}
	} while (Tecla != 13 && Tecla != 48);
}

void cServicos () {
    int Tecla;

	system("cls");
	Intanciar_campo();
	Resulte();

    do{
        Posicao(3,1);
        printf("Valor: R$ %.2f ", cValorServ + cValorProd);

        Posicao(26,5);
        printf("=====Servicos=====");

        Posicao(8,8);
        printf("<1> Banho  - R$ %.2f", cValores[0]);
        Posicao(8,9);
        printf("<2> Tosa  -  R$ %.2f", cValores[1]);
        Posicao(8,10);
        printf("<3> Vacina - R$ %.2f", cValores[2]);
        Posicao(8,12);
        printf("<Delete> Zerar os servicos selecionados");
		Posicao(8,13);
        printf("<0> Voltar ao menu");

        Posicao(6,19);
        printf("Pressione 'enter' para Finalizar todas as compras");

		do{
		    Tecla = 0;
            fflush(stdin);
            Tecla = getch ();
		} while (Tecla != 49 && Tecla != 50 && Tecla != 51 && Tecla != 13 && Tecla != 224 && Tecla != 48);//ASCII: 49=1  50=2  13=Enter  224=Delete  48=0

		if(Tecla == 49){
			cValorServ += cValores[0];
		}
		if(Tecla == 50){
			cValorServ += cValores[1];
		}
		if(Tecla == 51){
			cValorServ += cValores[2];
		}
		if(Tecla == 48){
			cMenu ();
		}
		if(Tecla ==224){
			cValorServ = 0;
		}
	} while (Tecla != 13 && Tecla != 48);
}

void gprodutos () {
    int Tecla;

	system("cls");
	Intanciar_campo();
	Resulte ();

    do{
        Posicao(3,1);
        printf("Valor: R$ %.2f ", gValorServ + gValorProd);

        Posicao(26,5);
        printf("=====Produtos=====");

        Posicao(8,8);
        printf("<1> Medicamento - R$ %.2f", gValores[3]);

        Posicao(8,9);
        printf("<2> Racao    -    R$ %.2f", gValores[4]);

        Posicao(8,11);
        printf("<Delete> Zerar os produtos selecionados");

		Posicao(8,12);
        printf("<0> Voltar ao menu");

        Posicao(6,19);
        printf("Pressione 'enter' para Finalizar todas as compras");

        do {
		    Tecla = 0;
            fflush(stdin);
            Tecla = getch ();
		} while (Tecla != 49 && Tecla != 50 && Tecla != 13 && Tecla != 224 && Tecla != 48);//ASCII: 49=1  50=2  13=Enter  224=Delete  48=0

		if(Tecla == 49){
			gValorProd += gValores[3];
		}
		if(Tecla == 50){
			gValorProd += gValores[4];
		}
		if(Tecla == 48){
			gMenu ();
		}
		if(Tecla ==224){
			gValorProd = 0;
		}
    } while (Tecla != 13 && Tecla != 48);
}

void cprodutos () {
    int Tecla;

	system("cls");
	Intanciar_campo();
	Resulte ();

    do{
        Posicao(3,1);
        printf("Valor: R$ %.2f ", cValorServ + cValorProd);

        Posicao(26,5);
        printf("=====Produtos=====");

        Posicao(8,8);
        printf("<1> Medicamento - R$ %.2f", cValores[3]);

        Posicao(8,9);
        printf("<2> Racao    -    R$ %.2f", cValores[4]);

        Posicao(8,11);
        printf("<Delete> Zerar os produtos selecionados");

		Posicao(8,12);
        printf("<0> Voltar ao menu");

        Posicao(6,19);
        printf("Pressione 'enter' para Finalizar todas as compras");

        do{
		    Tecla = 0;
            fflush(stdin);
            Tecla = getch ();
		} while (Tecla != 49 && Tecla != 50 && Tecla != 13 && Tecla != 224 && Tecla != 48);//ASCII: 49=1  50=2  13=Enter  224=Delete  48=0

		if(Tecla == 49){
			cValorProd += cValores[3];
		}
		if(Tecla == 50){
			cValorProd += cValores[4];
		}
		if(Tecla == 48){
			cMenu ();
		}
		if(Tecla ==224){
			cValorProd = 0;
		}
    } while (Tecla != 13 && Tecla != 48);
}

void PDC () {
	char comando[16];

	Posicao(3,1);
	printf("comando> ");

	fflush(stdin);
	gets(comando);

	if(comando[0] == 'A' && comando[1] == 'l' && comando[2] == 't' && comando[3] == 'V' && comando[4] == 'a' && comando[5] == 'l') {
        system("cls");
        AltVal();
        main();
        exit(0);
	} else if(comando[0] == 'e' && comando[1] == 'x' && comando[2] == 'i' && comando[3] == 't') {
		system("cls");
		main();
		exit(0);
	} else {
		system("cls");
		Intanciar_campo();
		Posicao(20,5);
		printf("=====Comando Invalido=====");
		PDC ();
	}
}

void AltVal () {
	int aux;
	int tecla;

    Intanciar_campo();
    Posicao(22,5);
    printf("=====Alterar Precos=====");
    Posicao(2,7);
    printf("Alterar precos para:");
    Posicao(2,8);
    printf("(G - gato  C - cachorro)");
    Posicao(23,7);
    fflush(stdin);
    gets(a);

    if(a[0] == 'g' || a[0] == 'G'){
    	while (aux == 0) {
    		Preco ();

	        system("cls");
	        Intanciar_campo();

	        Posicao(18,5);
	        printf("=====Alterar Precos - Gatos=====");

	        Posicao(10,8);
	        printf("(1)Medicamento - R$ %.2f", gValores[3]);
	        Posicao(10,9);
	        printf("(2)Racao       - R$ %.2f", gValores[4]);
	        Posicao(40,8);
	        printf("(3)Banho  - R$ %.2f", gValores[0]);
	        Posicao(40,9);
	        printf("(4)Tosa   - R$ %.2f", gValores[1]);
	        Posicao(40,10);
	        printf("(5)Vacina - R$ %.2f", gValores[2]);
			Posicao(40,11);
	        printf("(0)Cancela");

	        Posicao(2,21);
	        printf("Opcao escolhida: ");
	        scanf("%d",&x);

	        switch(x){
		        case 1:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&gModVal[0]);
		            break;
		        case 2:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&gModVal[1]);
		            break;
		        case 3:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&gModVal[2]);
		            break;
		        case 4:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&gModVal[3]);
		            break;
		        case 5:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&gModVal[4]);
		            break;
		        case 0:
		            //AltVal();
		            break;
		        default:
		            printf("Opcao invalida!");
		            break;
	        }

			if(x != 0) {
		        Posicao(18,17);
		        printf("=====Alterado com Sucesso!=====");
		    	Posicao(6,19);
				printf("Deseja alterar outros valores? <S>sim ou <N>nao ");
				do {
				tecla = 0;
				fflush(stdin);
				tecla=getch();
				} while (tecla != 115 && tecla != 110);

				if(tecla == 110) { ///S
					aux = 1;
				}
			} else {
				Posicao(6,19);
				printf("Sair do alterarador de valores? <S>sim ou <N>nao ");
				do {
				tecla = 0;
				fflush(stdin);
				tecla=getch();
				} while (tecla != 115 && tecla != 110);

				if(tecla == 115) { ///S
					aux = 1;
				}
			}
	    }
    } else if(a[0] == 'c' || a[0] == 'C'){
	    while (aux == 0) {
	    	Preco ();

	        system("cls");
	        Intanciar_campo();

	        Posicao(16,5);
	        printf("=====Alterar Precos - Cachorro=====");
	        Posicao(10,8);
	        printf("(1)Medicamento - R$ %.2f", cValores[3]);
	        Posicao(10,9);
	        printf("(2)Racao       - R$ %.2f", cValores[4]);
	        Posicao(40,8);
	        printf("(3)Banho  - R$ %.2f", cValores[0]);
	        Posicao(40,9);
	        printf("(4)Tosa   - R$ %.2f", cValores[1]);
	        Posicao(40,10);
	        printf("(5)Vacina - R$ %.2f", cValores[2]);
			Posicao(40,11);
	        printf("(0)Cancela");

	        Posicao(2,21);
	        printf("Opcao escolhida: ");
	        scanf("%d",&x);

	        switch(x){
		        case 1:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&cModVal[0]);
		            break;
		        case 2:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&cModVal[1]);
		            break;
		        case 3:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&cModVal[2]);
		            break;
		        case 4:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&cModVal[3]);
		            break;
		        case 5:
		            Posicao(40,21);
		            printf("Insira o novo valor: ");
		            scanf("%f",&cModVal[4]);
		            break;
		        case 0:
		            //AltVal();
		            break;
		        default:
		            printf("Opcao invalida!");
	        }
	        if(x != 0) {
		        Posicao(18,17);
		        printf("=====Alterado com Sucesso!=====");
		    	Posicao(6,19);
				printf("Deseja alterar outros valores? <S>sim ou <N>nao ");
				do {
				tecla = 0;
				fflush(stdin);
				tecla=getch();
				} while (tecla != 115 && tecla != 110);

				if(tecla == 110) { ///S
					aux = 1;
				}
			} else {
				Posicao(6,19);
				printf("Sair do alterarador de valores? <S>sim ou <N>nao ");
				do {
				tecla = 0;
				fflush(stdin);
				tecla=getch();
				} while (tecla != 115 && tecla != 110);

				if(tecla == 115) { ///S
					aux = 1;
				}
			}
	    }
    }
    system("cls");
	Intanciar_campo();
}

void Preco () {
	//Valor de produtos e servicos para Gatos
	if(a[0] == 'g' || a[0] == 'G') {
		//Sevicos
		gValores[0] = gModVal[2];		// Banho
		gValores[1] = gModVal[3];		// Tosa
		gValores[2] = gModVal[4];		// Vacina
		//produtos
		gValores[3] = gModVal[0];		// Medicamento
		gValores[4] = gModVal[1];		// Racao
	}
	//Valor de produtos e servicos para Cachorros
	if(a[0] == 'c' || a[0] == 'C') {
		//Sevicos
		cValores[0] = cModVal[2];		// Banho
		cValores[1] = cModVal[3];		// Tosa
		cValores[2] = cModVal[4];		// Vacina
		//produtos
		cValores[3] = cModVal[0];		// Medicamento
		cValores[4] = cModVal[1];		// Racao
	}
}

void IniciarSistema () {

	Posicao(2,3);
	printf("Especie do animal: ");

	Posicao(2,4);
	printf("(G - gato  C - cachorro)");

	Posicao(21,3);
	fflush(stdin);
	gets(a);

	Preco();

	if(a[0] == '@' && a[1] == 'c' && a[2] == 'o' && a[3] == 'm') {
		PDC ();
	} else if(a[0] == 'C' || a[0] == 'c') {
		Posicao(26,5);
		printf("=====Cachorro=====");

	} else if(a[0] == 'G' || a[0] == 'g') {
		Posicao(26,5);
		printf("======Gato======");
	} else {
		system("cls");
		Intanciar_campo();
		Posicao(26,5);
		printf ("Opcao invalida");
		IniciarSistema ();
	}
}

int Idade (int ano) {
	return 2017 - ano;
}

void Resulte () {

	Posicao(2,21);
	printf ("Nome: %s", NomeAnimal);

	Posicao(27,21);
	printf ("Raca: %s", raca);

	Posicao(55,21);
	if(Idade (dataDeNac) == 1) {
		printf ("Idade: %d ano", Idade (dataDeNac));
	} else {
		printf ("Idade: %d anos", Idade (dataDeNac));
	}
}

void gMenu () { // Produtos e Servicos
	int tecla=0;

	system("cls");
	Resulte ();
	Intanciar_campo();

	Posicao(32,8);
	printf("Menu:");

	Posicao(18,12);
	printf("<1>Produtos");

	Posicao(40,12);
	printf("<2>Servicos");

	do {
		tecla = 0;
		fflush(stdin);
		tecla = getch();
	} while (tecla != 49 && tecla != 50);

	if(tecla == 49) {
		Posicao(13,15);
		gprodutos ();
	}
	if (tecla == 50) {
		Posicao(13,15);
		gServicos ();
	}
}

void cMenu () { // Produtos e Serviços
	int tecla=0;

	system("cls");
	Resulte ();
	Intanciar_campo();

	Posicao(32,8);
	printf("Menu:");

	Posicao(18,12);
	printf("<1>Produtos");

	Posicao(40,12);
	printf("<2>Servicos");

	do {
		tecla = 0;
		fflush(stdin);
		tecla = getch();
	} while (tecla != 49 && tecla != 50);

	if(tecla == 49) {
		Posicao(13,15);
		cprodutos ();
	}
	if (tecla == 50) {
		Posicao(13,15);
		cServicos ();
	}
}

void cadastro () {		// cadastro e correcao de dados

	Posicao(26,6);
	printf("Cadastro do animal:");

	Posicao(2,8);
	printf("Nome do animal: ");
	fflush(stdin);    //Limpa o buffer do teclado
	fgets(NomeAnimal,16,stdin);

	Posicao(2,9);
	printf("Raca do animal: ");
	fflush(stdin);
	fgets(raca,16,stdin);

	Posicao(2,10);
	printf("Ano de nasc. do animal (apenas o ano): ");
	fflush(stdin);
	scanf("%d", &dataDeNac);

	if(dataDeNac > 2017) {
		system("cls");
		Intanciar_campo();
		Posicao(23,4);
		printf("=====Idade Invalida=====");
		cadastro ();
	}

	if(dataDeNac < 2000) {
		system("cls");
		Intanciar_campo();
		Posicao(23,4);
		printf("=====Idade Invalida=====");
		cadastro ();
	}

	Resulte ();

	int tecla;
	Posicao(6,19);
	printf("Deseja fazer alguma correcaos nos dados? <S>sim ou <N>nao ");

	do {
		tecla = 0;
		fflush(stdin);
		tecla=getch();
	} while (tecla != 115 && tecla != 110);

	if(tecla == 115) { ///S
		system("cls");
		Intanciar_campo();
		cadastro ();
	}
	/// N -> proxima void na main depois de cadastro
}
