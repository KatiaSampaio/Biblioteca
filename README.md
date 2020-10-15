# Biblioteca
Sistema de controle de biblioteca com CRUD na linguagem C++
#include<stdio.h>
#include<stdlib.h> //para system("cls") e system("pause")
#include<ctype.h> // para entender tantos letras maiúsculas quanto minúsculas
#include<string.h>
#include<locale.h>
#define TAM 1000
typedef struct {
	char autor[100],obra[50],editora[20],categoria[20];
	int ano_publi,cod;
	
	
}gestao;
main(){
	setlocale(LC_ALL,"");
	int controle=0,cod_livro=1,busca_cod;
	char menu;
	gestao livro[TAM];
	bool achou=false;
	do{
		printf("\t== Gestão de biblioteca ==\n");
		printf("\n1- Cadastrar");
		printf("\n2- Consultar");
		printf("\n3- Listar");
		printf("\n4- Editar Cadastro");
		printf("\n5- Excluir Livro");
		printf("\nS- Sair ");
		printf("\n\nSelecione a opção desejada: ");
		fflush(stdin);
		scanf("%c",&menu);
		menu=toupper(menu);
		switch(menu){
			case'1':
				system("cls");
				if(controle==TAM) printf("\n\t SEM ESPAÇO PARA NOVOS CADASTROS\n\n");
				else{
					printf("\t*CADASTRO DE LIVRO*");
					printf("\n\nNome do autor: ");
					fflush(stdin);
					gets(livro[controle].autor);
					printf("\nNome do livro: ");
					fflush(stdin);
					gets(livro[controle].obra);
					printf("\nEditora: ");
					gets(livro[controle].editora);
					printf("\nAno de publicação: ");
					scanf("%i",&livro[controle].ano_publi);
					printf("\n\nCategoria: ");
					fflush(stdin);
					gets(livro[controle].categoria);
					livro[controle].cod = cod_livro;
					printf("\nCódigo do Livro => %03i\n\n",cod_livro);
					cod_livro++;
					
					printf("\n\tCADASTRO REALIZADO COM SUCESSO!\n\n");
					controle++;
					system("pause");
					system("cls");
				} 
				break;
			case '2':
				achou = false;
				busca_cod = 0;
				system("cls");
				if(controle==0)  {
					printf("\n\tNÃO HÁ LIVROS CADASTRADOS!\n\n");
				}
				else{
					printf("\n\t*CONSULTAR DISPONIBILIDADE DE LIVRO*\n\n");
					printf("Informe o Código do livro: ");
					scanf("%i",&busca_cod);
					for(int x=0; x<controle; x++){
						if(livro[x].cod == busca_cod && achou == false){
							achou = true;
							printf("\nTitulo: %s",livro[x].obra);
							printf("\nAutor: %s",livro[x].autor);
							printf("\nEditora: %s",livro[x].editora);
							printf("\nAno de Publicação: %i",livro[x].ano_publi);
							printf("\nCategoria: %s",livro[x].categoria);
							printf("\nCódigo: %03i",livro[x].cod);
							printf("\n---------------------\n\n");
							break;
						}
					}
					if(achou == false){
						printf("\n\tCódigo inexistente!\n\n");
					}					
				}
				system("pause");
				system("cls");
				break;
			case '3':
				system("cls");
				if(controle==0)  printf("\n\tNÃO HÁ LIVROS CADASTRADOS!\n\n");
				else{
					printf("\n\t*LIVROS CADASTRADOS*\n");
					for(int x=0;x<controle;x++){
						printf("\nTitulo: %s",livro[x].obra);
						printf("\nAutor: %s",livro[x].autor);
						printf("\nEditora: %s",livro[x].editora);
						printf("\nAno de Publicação: %s",livro[x].ano_publi);
						printf("\nCategoria: %s",livro[x].categoria);
						printf("\nCódigo: %03i",livro[x].cod);
						printf("\n---------------------\n\n");
					}
				}
				system("pause");
				system("cls");
				break;
			//4- Editar Cadastro
			case '4':
				achou = false;
				busca_cod = 0;
				system("cls");
				if(controle==0)  {
					printf("\n\tNÃO HÁ LIVROS CADASTRADOS!\n\n");
				}
				else{
					//Buscar codigo do cadastro que o usuario quer editar
					
					char autor_informado[100],obra_informada[50],editora_informada[20],categoria_informada[20];
					int ano_publi_informado,alteracao_confirmada;
				
								
					printf("\n\t*EDITAR CADASTRO DE LIVRO*\n\n");
					printf("Informe o Código do livro: ");
					scanf("%i",&busca_cod);
					//encontrar na minha biblioteca o livro desejado
					for(int x=0; x<controle; x++){
						if(livro[x].cod == busca_cod && achou == false){
							achou = true;
							printf("\n Cadastro atual do livro %03i \n",livro[x].cod);
							printf("\nTitulo: %s",livro[x].obra);
							printf("\nAutor: %s",livro[x].autor);
							printf("\nEditora: %s",livro[x].editora);
							printf("\nAno de Publicação: %s",livro[x].ano_publi);
							printf("\nCategoria: %s",livro[x].categoria);
							
							//receber os valores que serao alterados
							printf("\n\nInforme os dados corretamente: \n\n");
							
							printf("\n\nNome do autor: ");
							fflush(stdin);
							gets(autor_informado);
							printf("\nNome do livro: ");
							fflush(stdin);
							gets(obra_informada);
							printf("\nEditora: ");
							gets(editora_informada);
							printf("\nAno de publicação: ");
							scanf("%i",&ano_publi_informado);
							printf("\n\nCategoria: ");
							fflush(stdin);
							gets(categoria_informada);
							
							//confirmar a alteração
							printf("Confirmar alterações? \n1-SIM\n2-NÃO\n");
							scanf("%i",&alteracao_confirmada);
							
							if(alteracao_confirmada == 1)
							{
								// finalizar a alteração	
								strcpy(livro[x].autor, autor_informado);
								strcpy(livro[x].obra, obra_informada);
								strcpy(livro[x].editora, editora_informada);
								livro[x].ano_publi = ano_publi_informado;
								strcpy(livro[x].categoria, categoria_informada);
								
								printf("\n\tALTERAÇÃO EFETUADA COM SUCESSO!\n");
							}else {
								printf("\n\tAlteração cancelada!\n");
							}
							break;
						}
					}
					
					//caso eu nao encontre, informar o usuario
					if(achou == false){
						printf("\n\tCódigo inexistente!\n\n");
					}		
				}
				system("pause");
				system("cls");
				break;
			//5- Excluir Livro
			case '5':
				achou = false;
				busca_cod = 0;			
				system("cls");
				
				if(controle==0)  {
					printf("\n\tNÃO HÁ LIVROS CADASTRADOS!\n\n");
				}
				else{
					printf("\n\t*EXCLUIR CADASTRO DE LIVRO*\n\n");
					printf("Informe o Código do livro a ser excluído: ");
					scanf("%i",&busca_cod);
					
					
					for(int x=0;x<controle;x++){
						if(livro[x].cod == busca_cod){
							achou = true;
							printf("\n Cadastro atual do livro %03i \n",livro[x].cod);
							printf("\nTitulo: %s",livro[x].obra);
							printf("\nAutor: %s",livro[x].autor);
							printf("\nEditora: %s",livro[x].editora);
							printf("\nCategoria: %s",livro[x].categoria);
							
							int alteracao_confirmada;
							printf("\nConfirmar exclusão? \n1-SIM\n2-NÃO\n");
							scanf("%i",&alteracao_confirmada);
							
							if(alteracao_confirmada == 1)
							{
								for(int k=x; k<controle; k++){
									livro[k]=livro[k+1];		
								}
								controle--;
								printf("\n\tLIVRO EXCLUÍDO COM SUCESSO! \n");
							}
							else {
								printf("\n\tExclusão cancelada!\n");
							}
							break;
						}
					}
					
					if(achou == false){
						printf("\n\tCódigo inexistente!\n\n");
					}
				}
				system("pause");
				system("cls");
				break;
			case 'S':
				break;
			default:
				printf("\n\tOpção inválida!\n\n");
				system("pause");
				system("cls");
				break;
			
		}
		
	}while(menu!='S');
	system("cls");
}
