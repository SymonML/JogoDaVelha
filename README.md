# JogoDaVelha
Projeto pessoal em andamento... 

using System;
using System.Collections.Generic;
using System.Linq;

class JogoDaVelha
{
    static char[,] tabuleiro = {
                { '1', '2', '3' },
                { '4', '5', '6' },
                { '7', '8', '9' }
        };

    static int Jogadas = 0;
    static char JogadorAtual = 'X';

    static void MostrarTabuleiro()
    {
        Console.WriteLine("JOGO DA VELHA DO SYMINHO\n");
        Console.WriteLine($" {tabuleiro[0, 0]} | {tabuleiro[0, 1]} | {tabuleiro[0, 2]} ");
        Console.WriteLine("---+---+---");
        Console.WriteLine($" {tabuleiro[1, 0]} | {tabuleiro[1, 1]} | {tabuleiro[1, 2]} ");
        Console.WriteLine("---+---+---");
        Console.WriteLine($" {tabuleiro[2, 0]} | {tabuleiro[2, 1]} | {tabuleiro[2, 2]} ");
    }

    static void Jogar()
    {
        Console.WriteLine($"Jogador {JogadorAtual}, escolha uma opção de 1 a 9: ");
        string opcao = Console.ReadLine();

        if (!int.TryParse(opcao, out int posicao) || posicao < 1 || posicao > 9)
        {
            Console.WriteLine("[ERROR] Opção inválida, pressione ENTER para recomeçar!");
            Console.ReadLine();
            return;
        }

        int linha = (posicao - 1) / 3;
        int coluna = (posicao - 1) % 3;

        if (tabuleiro[linha, coluna] == 'X' || tabuleiro[linha, coluna] == 'O')
        {
            Console.WriteLine("Esta posição já foi escolhida. Por gentileza, pressione ENTER para escolher outra opção!");
            Console.ReadLine();
            return;
        }
        tabuleiro[linha, coluna] = JogadorAtual;
        Jogadas++;
    }

    static bool VerificVencedor()
    {
        //Verifica Linhas e Colunas
        for (int i = 0; i < 3; i++)
        {
            if (tabuleiro[i, 0] == JogadorAtual && tabuleiro[i, 1] == JogadorAtual && tabuleiro[i, 2] == JogadorAtual)
            {
                return true;
            }
            if (tabuleiro[0, i] == JogadorAtual && tabuleiro[1, i] == JogadorAtual && tabuleiro[2, i] == JogadorAtual)
            {
                return true;
            }
        }

        if (tabuleiro[0, 0] == JogadorAtual && tabuleiro[1, 1] == JogadorAtual && tabuleiro[2, 2] == JogadorAtual)
        {
            return true;
        }
        if (tabuleiro[0, 2] == JogadorAtual && tabuleiro[1, 1] == JogadorAtual && tabuleiro[2, 0] == JogadorAtual)
        {
            return true;
        }
        return false;
    }
    static void AlternarJogador()
    {
        JogadorAtual = (JogadorAtual == 'X') ? 'O' : 'X';
    }

      static void Main()
    {
        while (true)
        {
            Console.Clear();
            ;//Menu();
            MostrarTabuleiro();
            Jogar();
            if (VerificVencedor())
            {
                Console.Clear();
                MostrarTabuleiro();
                Console.WriteLine($"\nParabéns jogador {JogadorAtual} venceu!");
                break;
            }
            if (Jogadas == 9)
            {
                Console.Clear();
                MostrarTabuleiro();
                Console.WriteLine("\nEmpate!");
                break;
            }
            AlternarJogador();
        }
    }
}
