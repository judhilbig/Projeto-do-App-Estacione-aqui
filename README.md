# Projeto-do-App-Estacione-aqui
Projeto da interface de um App para vagas de estacionar/faculdade-Bsi
[script.1.js](https://github.com/user-attachments/files/26716099/script.1.js)
// Autor: Julia Donada Hilbig

let wins = 0;
let draws = 0;
let losses = 0;
document.getElementById("tempo").textContent = ""; // Deixando o texto do tempo invisivel

// Funcao para o computador escolher uma opcao aleatoria de jogada
function getComputerChoice() {
    const choices = ["pedra", "papel", "tesoura", "lagarto", "spock"];
    const randomNumber = Math.floor(Math.random() * 5);
    return choices[randomNumber];
}

// Essa função irá obter a escolha feita pelo jogador e pelo computador(aleatória) e, de acordo com as regras, determinar o vencedor
function determineWinner(playerChoice, computerChoice) {
    if (playerChoice === computerChoice) {
        draws++;
        return "Empate!"
    } else if (
        (playerChoice === "pedra" && computerChoice === "tesoura") ||
        (playerChoice === "papel" && computerChoice === "pedra") ||
        (playerChoice === "tesoura" && computerChoice === "papel") ||
        (playerChoice === "pedra" && computerChoice === "lagarto") ||
        (playerChoice === "lagarto" && computerChoice === "spock") ||
        (playerChoice === "spock" && computerChoice === "tesoura") ||
        (playerChoice === "tesoura" && computerChoice === "lagarto") ||
        (playerChoice === "lagarto" && computerChoice === "papel") ||
        (playerChoice === "papel" && computerChoice === "spock") ||   
        (playerChoice === "spock" && computerChoice === "pedra")
    ) {
        wins++;
        return "Voce venceu!";
    } else {
        losses++;
        return "Voce perdeu!";
    }
}

// Atualizando a pontuacao de ganhos, perdas e empates
function updateScore() {
    document.getElementById("wins").textContent = wins;
    document.getElementById("draws").textContent = draws;
    document.getElementById("losses").textContent = losses;
}


function playerChoiceHandler(playerChoice) {
    // Chama as funcoes para obter a jogada do computador e determinar o vencedor da rodada
    const computerChoice = getComputerChoice();    
    const result = determineWinner(playerChoice, computerChoice);
    document.getElementById("playerChoice").textContent = playerChoice;

    let segundos = 3;
    function contagemRegressiva() {
      if (segundos > 0) {
        document.getElementById("tempo").textContent = segundos;
        segundos--;
        setTimeout(contagemRegressiva, 1000); // Contagem regressiva de 3 segundos (1s * 3)
      } else {
        document.getElementById("tempo").textContent = "Tempo esgotado!";
        document.getElementById("computerChoice").textContent = computerChoice;
        document.getElementById("result").textContent = result;
        updateScore();
      }
    }    
    contagemRegressiva();        
}


document.getElementById("pedra").addEventListener("click", () => playerChoiceHandler("pedra"));
document.getElementById("papel").addEventListener("click", () => playerChoiceHandler("papel"));
document.getElementById("tesoura").addEventListener("click", () => playerChoiceHandler("tesoura"));
document.getElementById("lagarto").addEventListener("click", () => playerChoiceHandler("lagarto"));
document.getElementById("spock").addEventListener("click", () => playerChoiceHandler("spock"));

document.getElementById("reset").addEventListener("click", () => {
    wins = 0;
    draws = 0;
    losses = 0;
    updateScore();
    document.getElementById("playerChoice").textContent = "";
    document.getElementById("computerChoice").textContent = "";
    document.getElementById("result").textContent = "";
    document.getElementById("tempo").textContent = ""
});
