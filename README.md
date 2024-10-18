import Foundation
// Estrutura para armazenar dados de usuário
struct Usuario {
    var nome: String
    var senha: String
}
// Banco de dados simples para logins
var usuarios: [Usuario] = []
// Função de registro de novo usuário
func registrarUsuario() {
    print("Nome do Herói (Marvel ou DC): ", terminator: "")
    guard let nome = readLine() else { return }

    print("Senha: ", terminator: "")
    guard let senha = readLine() else { return }

    let novoUsuario = Usuario(nome: nome, senha: senha)
    usuarios.append(novoUsuario)
    print("Usuário \(nome) registrado com sucesso!\n")
}
// Função de login
func loginUsuario() {
    print("Nome do Herói: ", terminator: "")
    guard let nome = readLine() else { return }

    print("Senha: ", terminator: "")
    guard let senha = readLine() else { return }

    if let _ = usuarios.first(where: { $0.nome == nome && $0.senha == senha }) {
        print("Login bem-sucedido! Bem-vindo, \(nome)!\n")
    } else {
        print("Nome ou senha inválidos.\n")
    }
}
// Função para substituir palavras em arquivos de texto
func substituirPalavra(_ caminho: String, _ palavraAntiga: String, _ palavraNova: String) {
    do {
        var conteudo = try String(contentsOfFile: caminho)
        conteudo = conteudo.replacingOccurrences(of: palavraAntiga, with: palavraNova)
        try conteudo.write(toFile: caminho, atomically: true, encoding: .utf8)
        print("Palavra '\(palavraAntiga)' substituída por '\(palavraNova)'.")
    } catch {
        print("Erro ao manipular o arquivo.")
    }
}
// Menu principal do programa
func menu() {
    while true {
        print("""
        1. Registrar novo usuário
        2. Fazer login
        3. Substituir palavra em arquivo
        4. Sair
        Escolha uma opção:
        """, terminator: "")

        guard let escolha = readLine(), let opcao = Int(escolha) else { continue }

        switch opcao {
        case 1:
            registrarUsuario()
        case 2:
            loginUsuario()
        case 3:
            print("Digite o caminho do arquivo: ", terminator: "")
            if let caminho = readLine() {
                print("Palavra a substituir: ", terminator: "")
                if let palavraAntiga = readLine() {
                    print("Nova palavra: ", terminator: "")
                    if let palavraNova = readLine() {
                        substituirPalavra(caminho, palavraAntiga, palavraNova)
                    }
                }
            }
        case 4:
            print("Saindo...")
            return
        default:
            print("Opção inválida.")
        }
    }
}
// Inicia o programa
menu()
